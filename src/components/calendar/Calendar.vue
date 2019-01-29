<template>
    <div class="calendar">
        <day v-for="(day, index) in days" :day="day" :key="index" :month="month"></day>
    </div>
</template>

<script>
import Day from './Day.vue';

export default {
    components: {
        Day
    },
    props: ['month'],
    computed: {
        days() {
            const amountOfDays = this.amountOfDays(new Date());
            const days = [];

            for (let index = 0; index < amountOfDays; index++) {
                days[index] = index + 1;
            }

            return days;
        }
    },
    methods: {
        amountOfDays(date) {
            return new Date(date.getFullYear(), date.getMonth() + 1, 0).getDate();
        }
    }
}
</script>

<style lang="scss" scoped>
    .calendar {
        margin: 0 auto;
        width: 600px;
        max-width: 100%;
        margin-top: 10px;
        display: flex;
        flex-wrap: wrap;
        align-content: baseline;
        justify-content: space-between;
    }
</style>