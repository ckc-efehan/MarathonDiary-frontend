<template>
  <div id="app">
    <LoginView />
  </div>
</template>

<script>
import LoginView from './views/LoginView.vue';

export default {
  name: 'App',
  components: {
    LoginView
  }
}
</script>

<style src="./assets/appStyles.css"></style>