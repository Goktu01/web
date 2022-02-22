<template>
  <form @submit.prevent="onSubmit" class="login-form">
    <h3>Register Page</h3>
    <div class="form-log">
      <label>Username </label>
      <input
        type="text"
        name="username"
        v-model="username"
        placeholder="Enter Username"
      />
    </div>
    <div class="form-log">
      <label>Password</label>
      <input
        type="password"
        name="password"
        v-model="password"
        placeholder="Enter password"
      />
    </div>
    <div class="login-check">
      <button type="submit" class="btn-check">Register</button>
    </div>
  </form>
</template>
<script>
export default {
  name: "Login",
  data() {
    return {
      name: "",
      password: "",
      users: [],
    };
  },
  created() {},

  methods: {
    async addUsers(users) {
      await fetch("api/users", {
        method: "POST",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(users),
      });

      // body: JSON.stringify(this.user),
      this.$router.push("/");
    },

    onSubmit(e) {
      e.preventDefault();
      if (this.username === "" || this.password === "") {
        alert("Compelete the missing part");
        return;
      }
      const newUser = {
        username: this.username,
        password: this.password,
      };
      this.addUsers(newUser);
      this.text = "";
      this.passw = "";
    },
  },
};
</script>
  
<style scoped>
.btn-check {
  display: block;
  width: 100%;

  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 20px 22px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
  text-align: center;
}

.login-form {
  margin-bottom: 40px;
}

.form-log {
  margin: 20px 0;
}

.form-log label {
  display: block;
}
.form-log input {
  width: 100%;
  height: 40px;
  padding: 3px 7px;
  font-size: 17px;
}
.login-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.login-check label {
  flex: 1;
}
.login-check input {
  flex: 2;
  height: 20px;
  text-align: center;
}
</style>