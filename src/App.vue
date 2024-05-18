<template src="./views/AppTemplate.html"></template>

<script>
import axios from 'axios';
import './assets/appStyles.css';
import TrainingEntries from './components/TrainingEntries.vue';

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
