<template>
  <div class="training-entries">
    <h2>Trainingsübersicht</h2>
    <ul>
      <li v-for="entry in entries" :key="entry.date">
        <div class="entry">
          <h3>{{ entry.date }}</h3>
          <p>Ziel-Zeit: <span class="bold-text">{{ entry.targetTime }} h</span></p>
          <p>Ziel-Kilometer: <span class="bold-text">{{ entry.targetKilometre }} km</span></p>
          <p>Gelaufene Kilometer: <span class="bold-text">{{ entry.kilometreRan }} km</span></p>
          <p>Benötigte Zeit: <span class="bold-text">{{ entry.timeRan }} h</span></p>
          <p>Ziel erreicht: <span class="bold-text">{{ entry.goalReached ? 'Ja' : 'Nein' }}</span></p>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'TrainingEntries',
  props: {
    entries: {
      type: Array,
      required: true
    }
  }
}
</script>