<template>
  <div id="app">
    <div class="container">
      <div class="row">
        <div class="col-12">
          <HelloWorld msg="Welcome to Your Vue.js + TypeScript App (component Paging)"/>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import HelloWorld from './components/hello-world/HelloWorld.vue'
// Bootstrap
import '../node_modules/bootstrap/dist/css/bootstrap.min.css'

@Component({
  components: {
    HelloWorld
  }
})
export default class App extends Vue {}
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
