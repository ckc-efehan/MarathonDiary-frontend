<template>
  <div class="newtrainingsentry">
    <h2>Neuer Trainingseintrag</h2>
    <span>Geben Sie hier ein wie viele Kilometer Ihr Ziel ist</span>
    <input type="zielZeit" placeholder="Ziel-Zeit">
    <span>Geben Sie hier ein in welcher Zeit (in Stunden) Sie das schaffen wollen</span>
    <input type="zielKilometer" placeholder="Ziel-Kilometer">
    <span>Geben Sie hier ein wie viel Kilometer Sie gerannt sind</span>
    <input type="gelaufeneKilometer" placeholder="Gelaufene Kilometer">
    <span>Geben Sie hier ein in welcher Zeit (in Stunden) Sie die Kilometer gelaufen sind</span>
    <input type="gelaufeneZeit" placeholder="Gelaufene Zeit">
    <button>Senden</button>
  </div>
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