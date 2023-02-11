<template>
  <div class="pendulum-canvas">
    <div
      class="pendulum-leg"
      :style="{
        height: long + '%',
        'animation-duration': fluctuations + 's',
      }"
    ></div>
  </div>
</template>

<script>
import {computed, toRef} from "vue";

export default {
  name: "PendulumComponent",
  props: ["L"],
  setup(props) {
    const g = 9.8;

    const long = toRef(props, "L");

    const fluctuations = computed(() => {
      return 20 * Math.PI * Math.sqrt(long.value / g);
    });

    return { g, fluctuations, long };
  },
};
</script>

<style scoped>
.pendulum-canvas {
  width: 50%;
  height: 50%;
  background: rgb(216, 175, 231);
  border-top: 2px solid black;
  position: relative;
}

.pendulum-leg {
  border: 1px solid black;
  position: absolute;
  right: 50%;
  animation: move;
  animation-iteration-count: infinite;
  transform-origin: 50% 0;
}

.pendulum-leg::after {
  content: "";
  position: absolute;
  height: 30px;
  width: 30px;
  background: yellow;
  top: 100%;
  left: -15px;
  border-radius: 50%;
}

@keyframes move {
  0%,
  100% {
    transform: translate(0, 0) rotate(40deg);
  }
  50% {
    transform: translate(0, 0) rotate(-40deg);
  }
}
</style>
