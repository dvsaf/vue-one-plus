<template>
  <div class="col-6 offset-3 pt-3 pb-3">
  <b-form @submit="submit" id="login">
    <b-form-group
        id="username-group"
        label="Username:"
        label-for="username-input"
        description="Enter username…"
    >
      <b-form-input
          id="username-input"
          v-model="username"
          type="text"
          placeholder="Enter username"
          required
      ></b-form-input>
    </b-form-group>
    <b-form-group
        id="password-group"
        label="Password:"
        label-for="password-input"
        description="Enter password…"
    >
      <b-form-input
          id="password-input"
          v-model="password"
          type="password"
          placeholder="Enter password"
          required
      ></b-form-input>
    </b-form-group>

    <b-button type="submit" variant="primary">Войти</b-button>
    
<!--    <label for="username">login</label>-->
<!--    <input id="username" type="text" class="form-control" v-model="username">-->
<!--    <br>-->
<!--    <label for="password">password</label>-->
<!--    <input id="password" type="password" class="form-control" v-model="password">-->
<!--    <br>-->
<!--    <b-button class="row ml-3 mr-1" @click="submit">Войти</b-button>-->
  </b-form>
  </div>
</template>

<script>
const authenticateUrl = "http://localhost:9001/tokens/authenticate";

export default {
  name: "Login",

  data() {
    return {
      username: null,
      password: null,
      accessToken: null
    }
  },

  methods: {
    submit() {
      console.log("submit");
      const self = this;

      fetch(authenticateUrl, {
        method: "POST",
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({
          username: this.username,
          password: this.password
        })
      })
          .then(response => {
            if (!response.ok) {
              throw Error(response.statusText);
            }
            return response.text();
          })
          .then(data => {
            console.log(data);
            self.accessToken = data;
            localStorage.jwtProfteh = self.accessToken;
            self.$router.push('/users');
          })
          .catch(error => console.log(error));
    }
  }
}
</script>

<style scoped>

</style>