<template>
  <div id="myDIV" class="header">
    <h2 style="margin: 5px">To Do List</h2>
    <img
      src="../assets/todo.png"
      alt=""
      srcset=""
      style="width: 100px; height: 100px"
    />
    <div class="inputStyle">
      <div class="inputWithCheckboxStyle" style="flex-grow: 3">
        <input
          type="text"
          v-model="taskName"
          id="myInput"
          placeholder="Add a task..."
          @keyup.enter="addClick"
          maxlength="100"
        />
        <div class="priority-checkbox">
          <label
            ><input
              type="checkbox"
              id="highPriority"
              name="highPriority"
              value="highPriority"
              v-model="highPriority"
            />High Priority</label
          >

          <label
            ><input
              type="checkbox"
              id="mediumPriority"
              name="mediumPriority"
              value="mediumPriority"
              v-model="mediumPriority"
            />
            Medium Priority</label
          >

          <label
            ><input
              type="checkbox"
              id="lowPriority"
              name="lowPriority"
              value="lowPriority"
              v-model="lowPriority"
            />
            Low Priority</label
          >
        </div>
      </div>
      <div>{{ characterCount }}/100</div>
      <div style="flex-grow: 1">
        <button
          @click="addClick"
          class="addBtn"
          :disabled="taskName.length <= 2"
        >
          Add
        </button>
      </div>
    </div>
  </div>
  <!-- <TaskList></TaskList> -->
</template>

<script>
/* eslint-disable */
// import TaskList from "../src/components/TaskList.vue";
export default {
  name: "AddTask",
  components: {
    // TaskList,
  },
  data() {
    return {
      taskName: "",
      taskList: [],
      highPriority: false,
      mediumPriority: false,
      lowPriority: false,
      priorityList: [],
      taskNameWithPriority: [],
    };
  },

  methods: {
    addClick() {
      if (!this.highPriority && !this.mediumPriority && !this.lowPriority) {
        alert("set task's priority");
      }

      // console.log("clicked");
      // console.log(this.taskName);

      // this.taskNameWithPriority.push({
      //   id: this.taskNameWithPriority.length + 1,
      //   task: this.taskName,
      //   priorityHigh: this.highPriority,
      //   priorityMedium: this.mediumPriority,
      //   priorityLow: this.lowPriority,
      //   doneTask:false,
      // });

      this.taskList.push(this.taskName);

      if (this.highPriority) {
        this.priorityList.push(this.highPriority);

        this.taskNameWithPriority.push({
          id: this.taskNameWithPriority.length + 1,
          task: this.taskName,
          priorityHigh: this.highPriority,
          priorityMedium: false,
          priorityLow: false,
          doneTask: false,
        });
      } else if (this.mediumPriority) {
        this.priorityList.push(this.mediumPriority);

        this.taskNameWithPriority.push({
          id: this.taskNameWithPriority.length + 1,
          task: this.taskName,
          priorityHigh: false,
          priorityMedium: this.mediumPriority,
          priorityLow: false,
          doneTask: false,
        });
      } else if (this.lowPriority) {
        this.priorityList.push(this.lowPriority);

        this.taskNameWithPriority.push({
          id: this.taskNameWithPriority.length + 1,
          task: this.taskName,
          priorityHigh: false,
          priorityMedium: false,
          priorityLow: this.lowPriority,
          doneTask: false,
        });
      }

      // console.log("taskList", this.taskList);
      // console.log("priority in addTask", this.taskNameWithPriority);

      this.$emit("taskWithPriority", this.taskNameWithPriority);

      this.taskName = "";
      this.highPriority = false;
      this.mediumPriority = false;
      this.lowPriority = false;
    },
  },

  computed: {
    characterCount() {
      return this.taskName.length;
    },
  },
};
</script>

<style scoped>
/* button[disabled] {
  background: #8795a1;
} */

button[disabled]:hover {
  /* background: #606f7b; */
  cursor: not-allowed;
}
.inputStyle {
  display: flex;
  flex-flow: row wrap;
  justify-content: space-around;
}

/* .inputStyleItem{
  flex-grow: 1;
} */

.inputWithCheckboxStyle {
  display: flex;
  flex-direction: column;
}
.priority-checkbox {
  font-size: small;
  /* background-color: rgb(57, 68, 64); */
  display: flex;
  flex-flow: row;
  justify-content: flex-start;
  padding: 5px;
}
.priority-checkbox > label {
  padding: 5px;
}
/* Style the header */
.header {
  background-color: #41b883;
  padding: 30px 40px;
  color: white;
  text-align: center;
}

/* Clear floats after the header */
/* .header:after {
  content: "";
  display: table;
  clear: both;
} */
/* Style the input */
input {
  margin: 0;
  border: none;
  border-radius: 0;
  /* width: 75%; */
  padding: 10px;
  /* float: left; */
  font-size: 16px;
}

/* Style the "Add" button */
.addBtn {
  padding: 8px;
  width: 100%;

  background-color: #35495e;
  color: #fff;
  /* float: left; */
  text-align: center;
  font-size: 16px;
  cursor: pointer;
  transition: 0.3s;
  border-radius: 0;
}

.addBtn:hover {
  background-color: #202c38;
}
</style>
