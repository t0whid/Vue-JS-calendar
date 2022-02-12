<template>
  <div class="container">
    <section>
      <h1 class="text-center">Vue JS Calendar</h1>
    </section>
    <h2>{{ currentMonthName }} {{ currentYear }}</h2>
    <section>
      <div class="days d-flex">
        <p class="text-center" v-for="(day, index) in days" :key="index">
          {{ day }}
        </p>
      </div>
    </section>
    <section>
      <div class="dates d-flex">
        <p class="text-center" v-for="day in firstDayOfMonth" :key="day"></p>
        <p :class="todayDate(date)" class="text-center" v-for="date in lastDateOfMonth" :key="date">
          {{ date }}
        </p>
      </div>
    </section>
    <section class="d-flex justify-content-between">
      <button @click="prev" class="btn btn-primary">Prev</button>
      <button @click="next" class="btn btn-primary">Next</button>
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      days: ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"],
      currentMonth: new Date().getMonth(),
      currentYear: new Date().getFullYear(),
      currentDay: new Date().getDate(),
    };
  },
  computed: {
    currentMonthName() {
      return new Date(
        this.currentYear,
        this.currentMonth,
        this.currentDay
      ).toLocaleString("default", { month: "long" });
    },
    lastDateOfMonth() {
      return new Date(this.currentYear, this.currentMonth + 1, 0).getDate();
    },
    firstDayOfMonth() {
      return new Date(this.currentYear, this.currentMonth, 1).getDay();
    },
  },
  methods: {
    prev() {
      if (this.currentMonth === 0) {
        this.currentYear--;
        this.currentMonth = 11;
      } else {
        this.currentMonth--;
      }
    },
    next() {
      if (this.currentMonth === 11) {
        this.currentYear++;
        this.currentMonth = 0;
      } else {
        this.currentMonth++;
      }
    },
    todayDate(date) {
      let calendarDate=new Date(this.currentYear, this.currentMonth, date).toDateString();
      let today= new Date().toDateString();

      return calendarDate===today ? ".text-primary bg-danger":"";
    },
  },
};
</script>

<style>
.days p,
.dates p {
  width: 14.28%;
}
.dates {
  flex-wrap: wrap;
}
</style>