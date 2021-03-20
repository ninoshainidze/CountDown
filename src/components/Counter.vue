<template>
  <div class="count_down">
    <div v-if="!expired">buy now</div>
    <div v-else>
      <h1>your time is up</h1>
      <!-- <video autoplay >
        <source src="../assets/10 Seconds of Weird Skull Zoom.mp4">
      </video> -->
    </div>
    <div class="time" v-if="loaded">
      <div class="days">
        {{ displayDays }}
        <p>days</p>
      </div>
      <span>:</span>
      <div class="hours">
        {{ displayHours }}
        <p>hours</p>
      </div>
      <span>:</span>
      <div class="minutes">
        {{ displayMinutes }}
        <p>minutes</p>
      </div>
      <span>:</span>
      <div class="seconds">
        {{ displaySeconds }}
        <p>seconds</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["year", "month", "date", "hour", "minute", "second", "millisecond"],
  data: () => {
    return {
      displayDays: 0,
      displayHours: 0,
      displayMinutes: 0,
      displaySeconds: 0,
      loaded: false,
      expired: false,
    };
  },
  computed: {
    seconds: () => 1000,
    minutes() {
      return this.seconds * 60;
    },
    hours() {
      return this.minutes * 60;
    },
    days() {
      return this.hours * 24;
    },
    end() {
      return new Date(
        this.year,
        this.month,
        this.date,
        this.hour,
        this.minute,
        this.second,
        this.millisecond
      );
    },
  },
  mounted() {
    this.showTime();
  },
  methods: {
    Numbers: (num) => (num < 10 ? "0" + num : num),
    showTime() {
      const timer = setInterval(() => {
        const now = new Date();
        // const end = new Date(2021, 2, 22, 10, 10, 10, 10);
        const distance = this.end.getTime() - now.getTime();

        if (distance < 0) {
          clearInterval(timer);
          this.expired = true;
          return;
        }

        const days = Math.floor(distance / this.days);
        const hours = Math.floor((distance % this.days) / this.hours);
        const minutes = Math.floor((distance % this.hours) / this.minutes);
        const seconds = Math.floor((distance % this.minutes) / this.seconds);

        this.displayMinutes = this.Numbers(minutes);
        this.displaySeconds = this.Numbers(seconds);
        this.displayHours = this.Numbers(hours);
        this.displayDays = this.Numbers(days);
        this.loaded = true;
      }, 1000);
    },
  },
};
</script>

<style scoped>
.time {
  display: flex;
  justify-content: center;
}
.days,
.hours,
.minutes,
.seconds,
span {
  margin: 10px;
}
h1 {
  color: red;
}
</style>
