<template>
  <div id="app">
    <training-entries :entries="trainingEntries"></training-entries>
  </div>
</template>

<script>
import TrainingEntries from './components/TrainingEntries.vue'

export default {
  name: 'App',
  components: {
    TrainingEntries
  },
  data() {
    return {
      trainingEntries: [
        { id: 1, date: '2023-05-01', kilometers: 5, time: '30 min', goalAchieved: true },
      ]
    }
  }
}
</script>
