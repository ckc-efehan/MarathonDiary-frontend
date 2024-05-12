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
        { id: 1, date: '2023-05-01',goalKilometers: 5, kilometers: 5,goalTime:30, time: '30 min', goalAchieved: true },
        { id: 2, date: '2023-05-02',goalKilometers: 11, kilometers: 10,goalTime: 90, time: '90 min', goalAchieved: false},
      ]
    }
  }
}
</script>
