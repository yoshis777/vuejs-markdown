<template>
  <div id="top">
    <div class="loading" v-if="!isLoginChecked">
      <i class="fa fa-spinner fa-spin fa-lg fa-5x"></i>
    </div>
    <h1><img alt="MyMarkdown" src="../assets/title-logo.png"></h1>
    <Home v-if="!isLogin"></Home>
    <Editor v-if="isLogin" :user="userData"></Editor>
    <router-link :to="{ name: 'terms' }">利用規約</router-link>
  </div>
</template>

<script>
  import Home from "../components/Home.vue";
  import Editor from "../components/Editor.vue";

  export default {
    name: "top",
    data() {
      return {
        isLogin: false,
        userData: null,
        isLoginChecked: false
      }
    },
    created: function() {
      firebase.auth().onAuthStateChanged(user => {
        //console.log(user);
        this.isLoginChecked = true;
        if(user) {
          this.isLogin = true;
          this.userData = user;
        } else {
          this.isLogin = false;
          this.userData = null;
        }
      });
    }
    ,
    components: {
      Home: Home,
      Editor: Editor
    }
  }
</script>

<style lang="scss">
  #top {
    font-family: "Avenir", Helvetica, Arial, sans-serif;
  }
  .loading {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: #eee;
    i {
      position: absolute;
      top: 50%;
      left: 50%;
      margin: -0.5em 0 0 -0.5em;
    }
  }
</style>
