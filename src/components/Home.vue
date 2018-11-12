<template>
  <div id="home">
    <button @click="googleLogin">Googleアカウントでログイン</button>
  </div>
</template>
<script>
  export default {
    name: "home",
    data() {
      return {}
    },
    methods: {
      googleLogin: function() {
        firebase
          .auth()
          .signInWithRedirect(new firebase.auth.GoogleAuthProvider());
      }
    }
  }
</script>
