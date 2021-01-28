<template>
  <div id="app">
    <Form />
  </div>
</template>

<script>
import Form from './components/Form.vue'

export default {
  name: 'App',
  components: {
    Form
  }
}
</script>

<style lang="scss">
@import "../public/normalize.css";
@import url('https://fonts.googleapis.com/css2?family=IBM+Plex+Sans:wght@400;500;700&display=swap');
html {
  background-color: #E5E5E5;
  font-family: "IBM Plex Sans";
  color: #2C2738;
}
#app {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
