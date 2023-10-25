<template>
<CalculationMachine/>
</template>

<script>
import CalculationMachine from './components/CalculationMachine.vue'

export default {
  name: 'App',
  components: {
    CalculationMachine
  }
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
