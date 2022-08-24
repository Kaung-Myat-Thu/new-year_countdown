<template>
  <div
    class="w-screen h-screen flex justify-center items-center flex-col text-slate-300"
  >
    <h1 class="text-3xl mb-4 font-bold font-serif text-center">
      New Year Countdown 🎉🎉🎉
    </h1>
    <Counter :year="2023" :month="0" :day="1" />
  </div>
</template>

<script>
import Counter from "@/components/Counter.vue";
export default {
  name: "App",
  components: {
    Counter,
  },
};
</script>

<style>
#app {
  background-image: url("./assets/bg_image.avif");
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
}
</style>
