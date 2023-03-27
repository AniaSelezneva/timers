<template>
  <div class="item" v-bind:class="{ 'active': stopwatch.running }">
    <p class="time">{{ formatTime(stopwatch.time) }}</p>
    <div class="buttons-container">
      <button @click="stopwatch.running ? pauseTimer() : startTimer()">
        <img v-if="stopwatch.running" v-bind:src="pauseIconPath" alt="Pause" />
        <img v-else v-bind:src="playIconPath" alt="Play" />
      </button>
      <button @click="stopTimer">
        <img v-bind:src="stopIconPath" alt="Stop" />
      </button>
    </div>
  </div>
</template>

<script>
import playIcon from '@/assets/playIcon.svg';
import activePlayIcon from '@/assets/activePlayIcon.svg';
import pauseIcon from '@/assets/pauseIcon.svg';
import activePauseIcon from '@/assets/activePauseIcon.svg';
import stopIcon from '@/assets/stopIcon.svg';
import activeStopIcon from '@/assets/activeStopIcon.svg';

export default {
  props: {
    index: Number,
  },
  data() {
    return {
      stopwatch: {
        time: 0,
        running: false,
        intervalId: null,
      },
    };
  },
  methods: {
    startTimer() {
      if (!this.stopwatch.running) {
        this.stopwatch.intervalId = setInterval(this.tick, 1000);
        this.stopwatch.running = true;
      }
    },
    pauseTimer() {
      clearInterval(this.stopwatch.intervalId);
      this.stopwatch.running = false;
    },
    stopTimer() {
      this.pauseTimer();
      this.stopwatch.time = 0;
    },
    formatTime(time) {
      const hours = Math.floor(time / 3600);
      const minutes = Math.floor((time % 3600) / 60);
      const seconds = time % 60;

      let timeString = '';
      if (hours > 0) {
        timeString += `${hours}:`;
      }

      if (minutes > 0 || hours > 0) {
        timeString += `${minutes.toString().padStart(2, '0')}:`;
      }

      timeString += `${seconds.toString().padStart(2, '0')}`;
      
      return timeString;
    },
    tick() {
      this.stopwatch.time += 1;
    },
  },
  computed: {
    playIconPath() {
      return this.stopwatch.running ? activePlayIcon : playIcon;
    },
    pauseIconPath() {
      return this.stopwatch.running ? activePauseIcon : pauseIcon;
    },
    stopIconPath() {
      return this.stopwatch.running ? activeStopIcon : stopIcon;
    },
  },
};
</script>

<style scoped>
.time, .buttons-container {
  flex: 1;
  margin: 0;
  display: flex;
  align-items: center;
}

.time {
    width: 100%;
    justify-content: center;
    border-bottom: 1px solid #9E9E9E;
}

.buttons-container {
  display: flex;
  gap: 48px;
}

.buttons-container button {
  border: none;
  padding: 0;
  background: none;
  color: #9E9E9E;
}

.active,
.active .buttons-container button {
  color: #FFFFFF;
}
.active .time {
  border-bottom: 1px solid #FFFFFF;
}
</style>

