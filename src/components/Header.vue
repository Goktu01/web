<template>
  <header>
    <h1>Task Tracker</h1>
    <Button
      v-show="homePage"
      @btn-click="$emit('toggle-add-task')"
      :text="showAddTask ? 'Close' : 'Add Task'"
      :color="showAddTask ? 'red' : 'green'"
    />

    <button v-on:click="showlogin">Log</button>
    <button v-on:click="showlogout">Logout</button>
  </header>
</template>

<script>
import Button from "./Button.vue";
import LoginVue from "./Login.vue";
export default {
  name: "Header",
  props: {
    title: String,
    showAddTask: Boolean,
  },
  components: {
    Button,
  },
  computed: {
    homePage() {
      if (this.$route.path === "/") {
        return true;
      } else {
        return false;
      }
    },
  },
  methods: {
    showlogin() {
      LoginVue;
      this.$router.push("./components/Login");
    },
    showlogout() {
      const data = fetch("api/users");
      localStorage.removeItem("userId", data.id);
    },
  },
};
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}

button {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: green;
  width: 50%;
  height: 40px;
  padding: 1px 5px;
  font-size: 20px;
  display: block;
}
</style>
