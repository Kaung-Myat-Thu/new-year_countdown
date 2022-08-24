<template>
  <div class="flex justify-around items-center" v-if="loaded">
    <div class="flex flex-col items-center">
      <div class="text-6xl font-semibold">{{ this.displayDays }}</div>
      <span class="block text-2xl">Days</span>
    </div>
    <span class="font-bold mx-4 mb-8 leading-snug text-6xl">:</span>
    <div class="flex flex-col items-center">
      <div class="text-6xl font-semibold">{{ this.displayHours }}</div>
      <span class="block text-2xl">Hours</span>
    </div>
    <span class="font-bold mx-4 mb-8 leading-snug text-6xl">:</span>
    <div class="flex flex-col items-center">
      <div class="text-6xl font-semibold">{{ this.displayMinutes }}</div>
      <span class="block text-2xl">Minutes</span>
    </div>
    <span class="font-bold mx-4 mb-8 leading-snug text-6xl">:</span>
    <div class="flex flex-col items-center">
      <div class="text-6xl font-semibold">{{ this.displaySeconds }}</div>
      <span class="block text-2xl">Seconds</span>
    </div>
  </div>
</template>

<script>
export default {
  props: ["year", "month", "day"],
  data() {
    return {
      displayDays: 0,
      displayHours: 0,
      displayMinutes: 0,
      displaySeconds: 0,
      loaded: false,
    };
  },
  computed: {
    second() {
      return 1000;
    },
    minute() {
      return this.second * 60;
    },
    hour() {
      return this.minute * 60;
    },
    _day() {
      return this.hour * 24;
    },
    end() {
      return new Date(this.year, this.month, this.day);
    },
  },
  mounted() {
    this.showRemining();
  },
  methods: {
    formatNum: (num) => (num < 10 ? "0" + num : num),
    showRemining() {
      const timer = setInterval(() => {
        const now = new Date();
        const distance = this.end.getTime() - now.getTime();
        if (distance < 0) {
          clearInterval(timer);
          this.loaded = true;
          return;
        }

        const days = Math.floor(distance / this._day);
        const hours = Math.floor((distance % this._day) / this.hour);
        const minutes = Math.floor((distance % this.hour) / this.minute);
        const seconds = Math.floor((distance % this.minute) / this.second);

        this.displayDays = this.formatNum(days);
        this.displayHours = this.formatNum(hours);
        this.displayMinutes = this.formatNum(minutes);
        this.displaySeconds = this.formatNum(seconds);
        this.loaded = true;
      }, 1000);
    },
  },
};
</script>
