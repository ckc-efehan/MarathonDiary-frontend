<template>
  <div id="app">
    <nav class="navbar">
      <div class="navbar-container">
        <h1>Meine Trainingsseite</h1>
        <ul class="navbar-nav">
          <li><a href="#"><i class="fas fa-home"></i> Abmelden</a></li>
        </ul>
      </div>
    </nav>
    <div class="content">
      <div class="newtrainingsentry">
        <h2>Neuer Trainingseintrag</h2>
        <span>Geben Sie hier ein in welcher Zeit (in Stunden) Sie das schaffen wollen</span>
        <input v-model="zielZeit" type="text" placeholder="Ziel-Zeit">
        <span>Geben Sie hier ein wie viele Kilometer Ihr Ziel ist</span>
        <input v-model="zielKilometer" type="text" placeholder="Ziel-Kilometer">
        <span>Geben Sie hier ein wie viel Kilometer Sie gerannt sind</span>
        <input v-model="gelaufeneKilometer" type="text" placeholder="Gelaufene Kilometer">
        <span>Geben Sie hier ein in welcher Zeit (in Stunden) Sie die Kilometer gelaufen sind</span>
        <input v-model="gelaufeneZeit" type="text" placeholder="Gelaufene Zeit">
        <button @click="submitEntry">Senden</button>
      </div>
      <div class="training-entries">
        <h2>Trainingsübersicht</h2>
        <ul v-if="trainingEntries.length > 0">
          <li v-for="entry in trainingEntries" :key="entry.id">
            <div class="entry">
              <h3>{{ entry.date }}</h3>
              <p>Ziel-Zeit: <span class="bold-text">{{ entry.targetTime }} h</span></p>
              <p>Ziel-Kilometer: <span class="bold-text">{{ entry.targetKilometre }} km</span></p>
              <p>Gelaufene Kilometer: <span class="bold-text">{{ entry.kilometreRan }} km</span></p>
              <p>Benötigte Zeit: <span class="bold-text">{{ entry.timeRan }} h</span></p>
              <p>Ziel erreicht: <span class="bold-text">{{ entry.goalReached ? 'Ja' : 'Nein' }}</span></p>
              <button @click="deleteEntry(entry.id)">Löschen</button>
            </div>
          </li>
        </ul>
        <p v-else>Keine Einträge vorhanden.</p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'TrainingEntries',
  data() {
    return {
      zielZeit: '',
      zielKilometer: '',
      gelaufeneKilometer: '',
      gelaufeneZeit: '',
      trainingEntries: []
    }
  },
  created() {
    this.fetchEntries();
  },
  methods: {
    async fetchEntries() {
      try {
        const response = await axios.get(import.meta.env.VITE_BACKEND_URL + '/entries');
        this.trainingEntries = response.data;
      } catch (error) {
        console.error(error);
      }
    },
    goalReached(targetTime, targetKilometer, timeRan, kilometreRan) {
      return (targetTime === timeRan && targetKilometer === kilometreRan) ||
          (timeRan < targetTime && kilometreRan > targetKilometer);
    },
    getCurrentDate() {
      const date = new Date();
      return date.toISOString().slice(0, 10);
    },
    async submitEntry() {
      const newEntry = {
        date: this.getCurrentDate(),
        targetTime: parseFloat(this.zielZeit),
        targetKilometre: parseFloat(this.zielKilometer),
        kilometreRan: parseFloat(this.gelaufeneKilometer),
        timeRan: parseFloat(this.gelaufeneZeit),
        goalReached: this.goalReached(parseFloat(this.zielZeit), parseFloat(this.zielKilometer), parseFloat(this.gelaufeneZeit), parseFloat(this.gelaufeneKilometer))
      };

      try {
        await axios.post(import.meta.env.VITE_BACKEND_URL + '/entries', newEntry);
        this.zielZeit = '';
        this.zielKilometer = '';
        this.gelaufeneKilometer = '';
        this.gelaufeneZeit = '';
        this.fetchEntries();
      } catch (error) {
        console.error('Error adding entry:', error);
      }
    },
    async deleteEntry(entryId) {
      try {
        await axios.delete(import.meta.env.VITE_BACKEND_URL + '/entries/' + entryId);
        this.fetchEntries();
      } catch (error) {
        console.error('Error deleting entry:', error);
      }
    }
  }
}
</script>

<style src="src/assets/trainingEntries.css"></style>
