<template>
  <div id="app">
     <p>{{ msg }}</p>
     <input type="text" v-model="msg"/>
     <h1 v-if="yes">yes</h1>
     <h1 v-if="no">no</h1>
     <p v-if="age >= 20">{{age}}</p>
     <p v-if="name.indexOf('j') >= 0">name:{{name}}</p>
     <!-- v-if v-show渲染加style，none -->
     <h1 v-show="yes">yes</h1>
     <h1 v-show="no">no</h1>
     <p v-show="age >= 20">{{age}}</p>
     <p v-show="name.indexOf('j') >= 0">name:{{name}}</p>
     <!-- v-else 必须跟在v-if和v-show的后面 -->
     <h1 v-if="age <= 20">msg：{{msg}}</h1>
     <p v-else>elseIfMsg:{{name}}</p>
  </div>
</template>

<script>

export default {
  name: 'app',
  data () {
    return {
      msg: ' 首页 ',
      yes: true,
      no: false,
      age: 28,
      name: 'jsons'
    }
  }
}

</script>

<style>
*{
  margin: 0;
  padding: 0;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  background: #ddd;
}

h1, h2 {
  font-weight: normal;
}
h1{
  color: #666;
}
ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
