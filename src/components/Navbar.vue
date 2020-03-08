<template>

  <ul class="container">

    <li><router-link to="/" class="navbar-link">Home</router-link></li>

    <template v-if="user.loggedIn">
      <li><div>{{user.data.displayName}}</div></li>
      <li @click.prevent="signOut"><a>Sign Out</a></li>
    </template>

    <template v-else>
      <li ><router-link to="login" class="nav-link">Login</router-link></li>
      <li ><router-link to="register" class="nav-link">Register</router-link></li>
    </template>

  </ul>

</template>
<script>
import { mapGetters } from "vuex";
import firebase from "firebase";
export default {
  computed: {
    ...mapGetters({
      // map `this.user` to `this.$store.getters.user`
      user: "user"
    })
  },
  methods: {
    signOut() {
      firebase
      .auth()
      .signOut()
      .then(() => {
        this.$router.replace({
          name: "home"
        });
      });
    }
  }
};
</script>

<style>
ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
  overflow: hidden;
  background-color: #dddddd;
}

li {
  float: left;
}

li a {
  display: block;
  padding: 8px;
}

li div {
  display: block;
  padding: 8px;
}

</style>
