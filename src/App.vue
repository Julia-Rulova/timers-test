<template>
  <section class="app">
    <TransitionGroup tag="ul" name="timers-list" class="timers">
      <timer-component
        v-for="(time, index) in timeArr"
        :key="index"
      ></timer-component>
      <li :key="Date.now()">
        <plus-timer @click="addTimer"></plus-timer>
      </li>
    </TransitionGroup>
  </section>
</template>

<script>
import PlusTimer from "./components/PlusTimer.vue";
import TimerComponent from "./components/TimerComponent.vue";

export default {
  name: "App",
  components: { PlusTimer, TimerComponent },

  data() {
    return {
      timeArr: [],
    };
  },
  methods: {
    addTimer() {
      this.timeArr.push(TimerComponent);
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

@font-face {
  font-family: "Gotham Pro";
  font-style: normal;
  font-weight: 400;
  font-display: swap;
  src: url("./assets/fonts/GothamPro.woff") format("woff");
}

.app {
  width: 100%;
  min-height: 100vh;
  background-color: #353638;
  padding: 72px 212px;
  display: flex;
  justify-content: center;
}

.timers {
  display: grid;
  grid-template-columns: repeat(3, 225px);
  grid-template-rows: repeat(auto-fit, 120px);
  gap: 45px 50px;
  list-style-type: none;
}

.timers-list-move,
.timers-list-enter-active,
.timers-list-leave-active {
  transition: all 0.5s ease;
}

.timers-list-enter-from,
.timers-list-leave-to {
  opacity: 0;
  transform: scale(0.6);
}

.timers-list-leave-active {
  position: absolute;
}

@media screen and (max-width: 800px) {
  .app {
    padding: 72px 135px;
  }

  .timers {
    grid-template-columns: repeat(2, 225px);
  }
}

@media screen and (max-width: 520px) {
  .app {
    padding: 72px 47px;
  }

  .timers {
    grid-template-columns: repeat(1, 225px);
    gap: 45px;
  }
}
</style>
