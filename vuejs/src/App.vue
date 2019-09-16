<template>
  <div id="app" >
    <div v-if="this.rows == null">
<p>Loading</p>
    </div>
    <div v-else>
<BookStore :rows="rows"></BookStore>
 
    </div>
  
  
  </div>
</template>

<script>
import Vue from "vue";
import axios from "axios";
import VueAxios from "vue-axios";

Vue.use(VueAxios, axios);

import BootstrapVue from "bootstrap-vue";

import "bootstrap/dist/css/bootstrap.css";
import "bootstrap-vue/dist/bootstrap-vue.css";

Vue.use(BootstrapVue);

import BookStore from "./components/BookStore.vue";
export default {
  name: "app",
  components: { 'BookStore': BookStore },
  data() {
    return {
      msg: "Welcome to Your Vue.js App",
      rows: null
    };
  },
  created() {
    fetch("https://api.jsonbin.io/b/5d6fd038fc5937640ce286a1")
      .then(res => {
        return res.json();
      })
      .then(res => {
        this.rows = res.books;
      });
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1,
h2 {
  font-weight: normal;
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
