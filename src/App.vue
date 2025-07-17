<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
     <HomePage/>
     
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import HomePage from './components/HomePage.vue';


export default {
  name: 'App',
  components: {
    // HelloWorld
    HomePage
    
  }
}
</script>

<style>
body,*,html {
  margin: 0;
  padding: 0;
}
element.style {
    height: auto;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;

}

</style>
