<template>
  <div class="training-entries">
    <h2>Trainingsübersicht</h2>
    <br>
    <ul>
      <li v-for="entry in entries" :key="entry.id">
        <div class="entry">
          <h3>{{ entry.date }}</h3>
          <p>Ziel-Kilometer: <span class="bold-text"> {{entry.goalKilometers}}</span></p>
          <p>Gelaufene Kilometer:<span class="bold-text"> {{ entry.kilometers }} km </span></p>
          <p>Ziel-Zeit: <span class="bold-text"> {{entry.goalTime}}</span></p>
          <p>Benötigte Zeit: <span class="bold-text"> {{ entry.time }}</span></p>
          <p>Ziel erreicht: <span class="bold-text">{{ entry.goalAchieved ? 'Ja' : 'Nein' }}</span></p>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import '@/assets/trainingEntries.css';


export default {
  name: 'TrainingEntries',
  props: {
    entries: Array
  }
}
</script>
