<template>
  <div class="newtrainingsentry">
    <h2>Neuer Trainingseintrag</h2>
    <span>Geben Sie hier ein wie viele Kilometer Ihr Ziel ist</span>
    <input v-model="zielZeit" type="text" placeholder="Ziel-Zeit">
    <span>Geben Sie hier ein in welcher Zeit (in Stunden) Sie das schaffen wollen</span>
    <input v-model="zielKilometer" type="text" placeholder="Ziel-Kilometer">
    <span>Geben Sie hier ein wie viel Kilometer Sie gerannt sind</span>
    <input v-model="gelaufeneKilometer" type="text" placeholder="Gelaufene Kilometer">
    <span>Geben Sie hier ein in welcher Zeit (in Stunden) Sie die Kilometer gelaufen sind</span>
    <input v-model="gelaufeneZeit" type="text" placeholder="Gelaufene Zeit">
    <button @click="submitEntry">Senden</button>
  </div>
  <div class="training-entries">
    <h2>Trainingsübersicht</h2>
    <ul>
      <li v-for="entry in entries" :key="entry.id">
        <div class="entry">
          <h3>{{ entry.date }}</h3>
          <p>Ziel-Zeit: <span class="bold-text">{{ entry.targetTime }} h</span></p>
          <p>Ziel-Kilometer: <span class="bold-text">{{ entry.targetKilometre }} km</span></p>
          <p>Gelaufene Kilometer: <span class="bold-text">{{ entry.kilometreRan }} km</span></p>
          <p>Benötigte Zeit: <span class="bold-text">{{ entry.timeRan }} h</span></p>
          <p>Ziel erreicht: <span class="bold-text">{{ entry.goalReached ? 'Ja' : 'Nein' }}</span></p>
          <button @click="deleteEntry">Löschen</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'TrainingEntries',
  props: {
    entries: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      zielZeit: '',
      zielKilometer: '',
      gelaufeneKilometer: '',
      gelaufeneZeit: ''
    }
  },
  methods: {
    goalReached(targetTime, targetKilometer, timeRan, kilometreRan) {
      return (targetTime === timeRan && targetKilometer === kilometreRan) ||
          (targetTime < timeRan || targetKilometer < kilometreRan);
    },
    submitEntry() {
      const newEntry = {
        targetTime: parseFloat(this.zielZeit),
        targetKilometre: parseFloat(this.zielKilometer),
        kilometreRan: parseFloat(this.gelaufeneKilometer),
        timeRan: parseFloat(this.gelaufeneZeit),
        goalReached: this.goalReached(parseFloat(this.zielZeit), parseFloat(this.zielKilometer), parseFloat(this.gelaufeneZeit), parseFloat(this.gelaufeneKilometer))
      };

      axios.post(import.meta.env.VITE_BACKEND_URL + '/entries', newEntry)
          .then(response => {
            this.$emit('entry-added', response.data);
            // Clear the input fields
            this.zielZeit = '';
            this.zielKilometer = '';
            this.gelaufeneKilometer = '';
            this.gelaufeneZeit = '';
          })
          .catch(error => {
            console.error('Error adding entry:', error);
          });
    },
    deleteEntry(entryId) {
      axios.delete(import.meta.env.VITE_BACKEND_URL + '/entries/' + entryId)
          .then(response => {
            // Do something after successful deletion, like updating the UI
          })
          .catch(error => {
            console.error('Error deleting entry:', error);
          });
    }
  }
}
</script>
