<template>
  <div class="slider-container">
    <input type="range" class="slider" :min="min" :max="max" :value="value" @change="sliderChange" />
  </div>
</template>

<script>
export default {
  name: "Slider",
  props: ["min", "max", "value"],
  methods: {
    sliderChange(e) {
      this.$emit("sliderChange", e.target.value);
    },
  },
};
</script>

<style scoped>
</style>