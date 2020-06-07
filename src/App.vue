<template>
  <div id="app">
    <Calculator />
  </div>
</template>

<script>
import Calculator from './components/Calculator.vue'

export default {
  name: 'App',
  components: {
    Calculator
  }
}
</script>

<style>
body {
    background-color: whitesmoke;
    font-family: 'Roboto', sans-serif;
}

input {
  padding: 15px;
  font-family: 'Roboto', sans-serif;
  border: 1px solid #ccc;
  border-radius: 3px;
  margin-bottom: 5px;
  width: 60%;
  margin-right: 10px;
  margin-left: 10px;
  font-size: 13px;
}

#app {
  box-shadow: 0px 1px 2px 1px rgba(0, 0, 0, 0.15);
  width: 350px;
  height: 500px;
  border-radius: 8px;
  margin: 0 auto;
  background-color: white;
  padding: 25px 20px;
}

.button {
  border: none;
  line-height: 1;
  display: inline-block;
  overflow: hidden;
  height: 44px;
  content: "";
  color: white;
  background: #61d5a7;
  cursor: pointer;
  box-sizing: border-box;
  font-weight: lighter;
  padding-bottom: 4px;
}

.label {
  color: #312d54;
  font-size: 12px;
  margin-bottom: 8px;
  margin-top: 8px;
  font-weight: 600;
}
</style>
