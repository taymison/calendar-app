<template>
    <div>
        <div :class="{'day':true, 'day--has_appointment':(appointments.length > 0)}" v-b-modal="idNewModal">
            {{ day }}
        </div>
        <b-modal :id="idNewModal" :title="titleModal">
            <b-alert variant="danger"
                dismissible
                :show="showDismissibleAlert"
                @dismissed="showDismissibleAlert=false">
                Already exists an appointment for this day.
            </b-alert>
            <b-table hover :fields="tableFields" :items="appointments" v-if="appointments.length > 0">
                <template slot="title" slot-scope="data">
                    {{ data.item.title }}
                </template>
                <template slot="actions" slot-scope="data">
                    <b-link href="#" v-b-modal="idEditModal">Edit</b-link> |
                    <b-link href="#" @click="removeAppointment(data.item.index)">Delete</b-link>
                </template>
            </b-table>
            <p v-else>No appointments are currently available.</p>
            <div slot="modal-footer">
                <b-btn variant="primary" @click="modalNewAppointment">New appointment</b-btn>
            </div>
        </b-modal>
        <b-modal ref="myModalRef" title="New Appointment">
            <div class="d-block text-center">
              <b-form-input v-model="newTitleAppointment" type="text" placeholder="New appointment"></b-form-input>
            </div>
            <div slot="modal-footer">
                <b-btn variant="primary" @click="hideModal(); newAppointment()">Ok</b-btn>
            </div>
        </b-modal>
        <b-modal :id="idEditModal" title="Edit Appointment" v-if="appointments.length > 0">
            <div class="d-block text-center">
              <b-form-input v-model="appointments[0].title" type="text" placeholder="Edit appointment"></b-form-input>
            </div>
            <div slot="modal-footer">
                <b-btn variant="primary" v-b-modal="idNewModal">Ok</b-btn>
            </div>
        </b-modal>
    </div>
    
</template>

<script>
export default {
    props: ['day', 'month'],
    data () {
        return {
            appointments: [],
            tableFields: ['title', {key: 'actions', label: 'Actions'}],
            showDismissibleAlert: false,
            newTitleAppointment: null,
        }
    },
    computed: {
        idNewModal() {
            return 'myModal' + this.day;
        },
        titleModal() {
            return 'Appointments on ' + this.month + ' ' + this.day;
        },
        idEditModal() {
            return 'editModal' + this.day;
        }
    },
    methods: {
        removeAppointment(index) {
            this.appointments.splice(index, 1);
        },
        modalNewAppointment() {
            if (this.checkIfAppointmentExists()) {
                this.showDismissibleAlert = true;
            } else {
                this.$refs.myModalRef.show();
            }
        },
        checkIfAppointmentExists() {
            return this.appointments.length > 0;
        },
        hideModal() {
            this.$refs.myModalRef.hide();
        },
        newAppointment() {
            this.appointments[0] = {
                index: 0,
                title: this.newTitleAppointment
            };

            this.newTitleAppointment = null;
        }
    }
}
</script>

<style lang="scss" scoped>
    .day {
        background-color: lightseagreen;
        height: 50px;
        width: 50px;
        line-height: 50px;
        text-align: center;
        margin: 5px;
        color: white;
        cursor: pointer;
        font-weight: bold;
        transition: 0.5s background-color;

        &--has_appointment, &:hover {
            background-color: seagreen;
        }
    }
</style>