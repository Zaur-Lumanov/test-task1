<template lang="pug">
	div.Login
		form.AuthForm(@submit="submit")
			b-card.AuthCard
				b-form-input(type="text" placeholder="Login" v-model="form.login" required)
				b-form-input(type="password" placeholder="Password" v-model="form.password" required)
				span.Restore Restore
				b-button.Login(type="submit" size="sm" variant="primary") Login
</template>

<script>
import Mock from "mockjs";
import axios from "axios";

window.axios = axios;
window.Mock = Mock;

const data = {
  form: {
    login: "",
    password: ""
  }
};

export default {
  name: "Login",
  data() {
    if (localStorage.login) {
      this.$router.push("main");
    }

    Mock.mock(/auth/, options => {
      return {
        token: "testToken",
        name: "Tim Cook"
      };
    });

    return data;
  },

  methods: {
    async submit(e) {
      e.preventDefault();

      const { data: response } = await axios.post("/auth", {
        login: this.form.login,
        password: this.form.password
      });

      if (response.token) {
        localStorage.login = this.form.login;

        this.$router.push("main");

        this.form.login = "";
        this.form.password = "";
      } else {
        alert("Invalid login or password");
      }

      return false;
    }
  }
};
</script>

<style scoped>
form.AuthForm {
  width: 300px;
  margin: 0 auto;
  margin-top: 100px;
}

.AuthCard input {
  margin: 10px 0;
}

span.Restore {
  float: left;
  cursor: pointer;
  color: #007bff;
  margin: 4px 0;
}

button.Login {
  float: right;
}
</style>
