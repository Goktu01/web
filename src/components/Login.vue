<template>
  <form @submit.prevent="login" class="login-form">
    <div class="form-log">
      <label>Username </label>
      <input
        type="text"
        name="text"
        v-model="username"
        placeholder="Enter Username"
      />
    </div>
    <div class="form-log">
      <label>Password</label>
      <input
        type="password"
        name="passw"
        v-model="password"
        placeholder="Enter password"
      />
    </div>
    <div class="login-check">
      <button type="submit" class="btn-check">Login</button>
    </div>
    <a href="/Register" >Have not an account?</a>
  </form>
</template>
<script>
export default {
  name: "Login",
  data() {
    return {
      text: "",
      name: "",
      password: "",
      users: [],
    };
  },
  created() {
    this.addUsers();
  },

  methods: {
    async login() {
      const user = {
        username: this.username,
        password: this.password,
      };

      const res = await fetch(`api/users?username=${user.username}`, {
        method: "GET",
        headers: {
          "Content-type": "application/json",
        },
      });
      const data = (await res.json())[0];

      if (data == null) {
        alert("This user not found");
        return;
      }

      if (user.password !== data.password) {
        alert("not equals");
        return;
      }
      localStorage.setItem("userId", data.id);
      this.$router.push("/");
    },

    async addUsers(newUser) {
      console.log(newUser);
      const res = await fetch("api/users", {
        method: "GET",
        headers: {
          "Content-type": "application/json",
        },
      });
      const data = await res.json();
      this.users = [...this.users, data];
      console.log(this.users);
    },

    onSubmit(e) {
      e.preventDefault();
      if (!this.text) {
        alert("Compelete the missing part");
        return;
      }
      const newUser = {
        text: this.text,
        passw: this.passw,
      };
      this.$emit("add-user", newUser);
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