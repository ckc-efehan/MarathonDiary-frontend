<template>
  <div class="training-entries">
    <h2>Trainingsübersicht</h2>
    <ul>
      <li v-for="entry in entries" :key="entry.id">
        <div class="entry">
          <h3>{{ entry.date }}</h3>
          <p>Gelaufene Kilometer: {{ entry.kilometers }} km</p>
          <p>Benötigte Zeit: {{ entry.time }}</p>
          <p>Ziel erreicht: <strong>{{ entry.goalAchieved ? 'Ja' : 'Nein' }}</strong></p>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'TrainingEntries',
  props: {
    entries: Array
  }
}
</script>
