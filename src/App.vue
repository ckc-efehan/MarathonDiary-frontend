<template src="./views/AppTemplate.html"></template>

<script>
import axios from 'axios';
import './assets/appStyles.css';
import './assets/trainingEntries.css';
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
      axios.get(import.meta.env.VITE_BACKEND_URL + '/entries')
          .then(function (response) {
            // handle success
            console.log(response);
            this.trainingEntries = response.data;
          }.bind(this))
          .catch(function (error) {
            // handle error
            console.log(error);
          })
          .finally(function () {
            // always executed
          });
    }
  }
}
</script>
