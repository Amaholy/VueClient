<template>
  <div id="app">
    <ClientForm />
  </div>
</template>

<script>
import ClientForm from './components/ClientForm.vue' // Импорт компонента ClientForm

export default {
  name: 'App',
  components: {
    ClientForm, // Регистрация компонента внутри App.vue
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
