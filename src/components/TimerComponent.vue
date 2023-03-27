<template>
  <li class="timer" :class="{ timer_off: timeState }">
    <div class="timer__container timer__container_text">
      <p class="timer__text">{{ hours }}</p>
      <p class="timer__text">{{ minutes }}</p>
      <p class="timer__text">{{ seconds }}</p>
    </div>
    <div class="timer__container">
      <button
        v-if="timeState"
        type="button"
        class="timer__pause"
        @click="handleTimerClick"
      />
      <button
        v-else
        type="button"
        class="timer__play"
        @click="handleTimerClick"
      />
      <button type="button" class="timer__reset" @click="clearTimer" />
    </div>
  </li>
</template>

<script>
export default {
  name: "TimerComponent",
  data() {
    return {
      timeState: false,
      hours: "",
      minutes: "",
      seconds: "00",
      totalTime: 0,
      timer: null,
    };
  },
  methods: {
    clearTimer() {
      clearInterval(this.timer);
      this.timeState = false;
      this.totalTime = 0;
      this.hours = "";
      this.minutes = "";
      this.seconds = "00";
    },
    handleTimerClick() {
      this.timeState = !this.timeState;
      if (this.timeState) {
        this.updateTimer();
      } else {
        clearInterval(this.timer);
      }
    },
    updateTimer() {
      this.timer = setInterval(() => {
        this.totalTime += 1;

        let hoursTime = Math.floor(this.totalTime / 60 / 60)
          .toString()
          .padStart(2, "0");
        let minutesTime = (Math.floor(this.totalTime / 60) - hoursTime * 60)
          .toString()
          .padStart(2, "0");
        let secondsTime = (this.totalTime % 60).toString().padStart(2, "0");

        if (this.totalTime >= 3600) {
          this.hours = hoursTime + ":";
          this.minutes = minutesTime + ":";
          this.seconds = secondsTime;
        } else if (this.totalTime > 60) {
          this.minutes = minutesTime + ":";
          this.seconds = secondsTime;
        } else {
          this.seconds = this.totalTime;
        }
      }, 1000);
    },
  },
};
</script>

<style>
.timer {
  width: 100%;
  height: 100%;
  background-color: #696969;
  display: flex;
  flex-direction: column;
}

.timer__container {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  height: 50%;
}

.timer__container_text {
  border-bottom: 1px solid #9e9e9e;
  font-family: "Gotham Pro";
  font-style: normal;
  font-weight: 400;
  font-size: 22px;
  line-height: 21px;
  color: #9e9e9e;
}

.timer_off .timer__container_text {
  border-bottom: 1px solid #fff;
  color: #fff;
}

.timer__play {
  background-color: #9e9e9e;
  clip-path: polygon(0 0, 0% 100%, 100% 50%);
  width: 17px;
  height: 20px;
  border: none;
  cursor: pointer;
}

.timer_off .timer__play {
  background-color: #fff;
}

.timer__pause {
  width: 10px;
  height: 20px;
  border: none;
  cursor: pointer;
  background-color: transparent;
  border-left: 3px solid #9e9e9e;
  border-right: 3px solid #9e9e9e;
}

.timer_off .timer__pause {
  border-left: 3px solid #fff;
  border-right: 3px solid #fff;
}

.timer__reset {
  width: 20px;
  height: 20px;
  background-color: #9e9e9e;
  margin-left: 48px;
  border: none;
  cursor: pointer;
}

.timer_off .timer__reset {
  background-color: #fff;
}
</style>