<template>
  <div class="slider-wrap">
    <input
      class="slider"
      type="range"
      :value="modelValue"
      @input="changeSize"
      min="5"
      max="100"
    />
  </div>
</template>

<script>
export default {
  name: "PendulumSlider",
  props: ["modelValue"],
  setup(props, { emit }) {
    function changeSize(e) {
      emit("update:modelValue", e.target.value);
    }
    return { changeSize };
  },
};
</script>
<style scoped>
.slider-wrap {
  width: 50%;
}
.slider {
  width: 100%;
}
</style>
