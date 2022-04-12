<template>
    <Movies>
    </Movies>
</template>

<script>
import Movies from "./components/Movies"

export default {
  name: 'App',

  components: { Movies }
}

</script>

<style>
body {
  background-color: #9cdbff;
}

#app {
  font-family: sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
h1 {
  border-bottom: 1px solid #ddd;
  display: inline-block;
  padding-bottom: 10px;
}

</style>