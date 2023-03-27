<template>
  <div class="wrapper">
    <div v-for="(timer, index) in timers" :key="index">
      <TimerComponent :index="index"></TimerComponent>
    </div>
    <button @click="addTimer" class="item">
      <img class="add-icon" src="@/assets/addIcon.svg" alt="Add" />
    </button>
  </div>
</template>

<script>
import TimerComponent from './components/TimerComponent.vue'

export default {
  components: {
    TimerComponent,
  },
  data() {
    return {
      timers: [],
    };
  },
  methods: {
    addTimer() {
      this.timers.push({ time: 0, running: false, intervalId: null });
    },
  }
};
</script>

<style>
.wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  row-gap: 45px;
  margin-top: 72px;
}

.item {
  width: 225px;
  height: 120px;
  background: #696969;
  color: #9E9E9E;
  border: none;
  
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.item img {
  cursor: pointer;
}

.add-icon:hover {
    content: url('@/assets/activeAddIcon.svg');
}

@media screen and (min-width: 768px) {
  .wrapper {
    flex-direction: row;
    flex-wrap: wrap;
    max-width: 500px;
    column-gap: 50px;
  }
}

@media screen and (min-width: 1024px) {
  .wrapper {
    max-width: 775px;
  }
}

body {
  margin: 0;
  background: #353638;
}

#app {
  display: flex;
  justify-content: center;
}
</style>
