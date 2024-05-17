<template>
  <div class="page-container">
    <div class="training-entries">
      <h2>Trainingsübersicht</h2>
      <br>
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

<style scoped>
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
