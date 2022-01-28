<template>
  <div id="app" class="container">
    <img src="./assets/logo.png" class="logo">
    <h1>To Do List</h1>
    <todolist></todolist>    
  
  </div>
</template>

<script>
import todolist from './components/todolist.vue'

export default {
  name: 'App',
  components: {
    todolist
  }
}
</script>
<style>
/* general styles for structuring my app vue */
* {
  box-sizing: border-box;
}
.container {
  max-width: 600px;
  margin: 0 auto;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: rgb(44, 62, 81);
  margin-top: 60px;
  font-size: 24px;
}
.logo {
  display: block;
  margin: 30px auto;
  height: 75px;
}
h1{
  text-align: center;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
}

</style>