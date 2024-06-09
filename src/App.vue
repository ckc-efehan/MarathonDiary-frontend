<template>
  <div id="app">
    <template v-if="isLoggedIn">
      <TrainingEntries />
    </template>
    <template v-else>
      <LoginView @loginSuccess="loginSuccess" />
    </template>
  </div>
</template>

<script>
import TrainingEntries from './components/TrainingEntries.vue';
import LoginView from './components/LoginView.vue';

export default {
  name: 'App',
  components: {
    TrainingEntries,
    LoginView
  },
  data() {
    return {
      isLoggedIn: false
    }
  },
  methods: {
    loginSuccess() {
      this.isLoggedIn = true;
    }
  }
}
</script>

<style>
/* Your global styles here */
</style>
