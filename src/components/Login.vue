<template>
  <div>
    <div v-if="error" class="alert alert-danger">{{error}}</div>

    <form action="#" @submit.prevent="submit">
      <label for="email" class="col-md-4 col-form-label text-md-right">Email</label><br/>
      <input
      id="email"
      type="email"
      class="form-control"
      name="email"
      value
      required
      autofocus
      v-model="form.email"
      /><br/>

      <label for="password" class="col-md-4 col-form-label text-md-right">Password</label><br/>
      <input
      id="password"
      type="password"
      class="form-control"
      name="password"
      required
      v-model="form.password"
      /><br/>

      <button type="submit" class="btn btn-primary">Login</button>
    </form>
  </div>
</template>

<script>
import firebase from "firebase";

export default {
  data() {
    return {
      form: {
        email: "",
        password: ""
      },
      error: null
    };
  },
  methods: {
    submit() {
      firebase
      .auth()
      .signInWithEmailAndPassword(this.form.email, this.form.password)
      .then(() => {
        this.$router.replace({ name: "Dashboard" });
      })
      .catch(err => {
        this.error = err.message;
      });
    }
  }
};
</script>
