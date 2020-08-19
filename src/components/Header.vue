<template>
  <div class="container__date">
    <p>
      <span>{{day}}</span>
      {{month}}
      <br />
      {{year}}
    </p>
    <p>{{currentDay}}</p>
  </div>
</template>

<script>
export default {
  name: "Header",
  data() {
    return {
      today: "",
      day: "",
      month: "",
      currentDay: "",
      monthNames: [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December"
      ],
      weekDays: [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday"
      ],
      year: ""
    };
  },
  created() {
    this.today = new Date();
    this.day = String(this.today.getDate()).padStart(2, "0");
    this.month = String(this.monthNames[this.today.getMonth()]).substring(0, 3);
    this.currentDay = String(this.weekDays[this.today.getDay()]);
    this.year = this.today.getFullYear();
  }
};
</script>

<style scoped>
.container__date {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-pack: justify;
  -ms-flex-pack: justify;
  justify-content: space-between;
}
.container__date p {
  font-size: 2rem;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  line-height: 23px;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
}
.container__date p span {
  line-height: normal;
  font-size: 4.5rem;
  margin-right: 5px;
  font-weight: bold;
}
</style>>
