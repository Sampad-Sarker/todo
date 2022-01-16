<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png" /> -->
  <AddTask @taskWithPriority="taskAndPriority"></AddTask>
  <TaskList :getTask="getTask"></TaskList>
  <!-- <HelloWorld msg="Welcome to Your Vue.js App" /> -->
</template>

<script>
import AddTask from "../src/components/AddTask.vue";
import TaskList from "../src/components/TaskList.vue";
// import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  components: {
    AddTask,
    TaskList,
    // HelloWorld,
  },
  emits: ["taskWithPriority"],

  data() {
    return {
      getTaskName: "",
      getTask: {},
    };
  },
  methods: {
    taskAndPriority(taskWithPriority) {
      console.log("in App:", taskWithPriority);
      // this.getTask.push(taskWithPriority);

      [this.getTask] = [taskWithPriority];
      console.log("getTask in app", this.getTask);


      // this.getTaskList.reverse();
    },
  },
};
</script>

<style>
/* Include the padding and border in an element's total width and height */
/* * {
  box-sizing: border-box;
} */

/* Remove margins and padding from the list */
ul {
  margin: 0;
  padding: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  box-sizing: border-box;
}
</style>
