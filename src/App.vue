<template>
  <div id="app">
    <training-entries :entries="trainingEntries"></training-entries>
  </div>
</template>

<script>
import axios from 'axios';
import TrainingEntries from './components/TrainingEntries.vue'

export default {
  name: 'App',
  components: {
    TrainingEntries
  },
  data() {
    return {
      trainingEntries: []
    }
  },
  created() {
    this.fetchEntries();
  },
  methods: {
    fetchEntries() {
      axios.get('http://localhost:8080/entries')
          .then(response => {
            this.trainingEntries = response.data;
          })
          .catch(error => {
            console.error("There was an error fetching the entries:", error);
          });
    }
  }
}
</script>

<style>
body {
  background: linear-gradient(to right, #c9d6ff, #ffffff);
  margin: 0;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

#app {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
}

.page-container {
  align-self: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
  width: 100vw;
  background: inherit;
}

.training-entries {
  background-color: #ffffff;
  padding: 20px;
  border-radius: 20px;
  width: 20%;
  box-shadow: 0px 8px 16px rgba(0, 0, 0, 0.2);
}

.training-entries h2 {
  color: #000000;
  text-align: center;
}

.training-entries ul {
  list-style-type: none;
  padding: 0;
}

.training-entries li {
  margin-bottom: 10px;
  border-bottom: 1px solid #ccc;
  padding-bottom: 10px;
}

.entry h3 {
  color: #007BFF;
}

.entry p {
  color: #666;
  margin: 5px 0;
}

.bold-text {
  font-weight: bold;
}
</style>

