<template>
  <p v-if="!(getTask.length > 0)">Yet no task added</p>
  <ul id="myUL">
    <li
      v-for="(task, index) in getTask"
      :key="index"
      :class="{
        priorityHigh: task.priorityHigh,
        priorityMedium: task.priorityMedium,
        priorityLow: task.priorityLow,
      }"
    >
      <div
        @click="strikeText(index)"
        :class="{ checked: task.doneTask }"
        style="flex-grow: 1; text-transform: capitalize"
      >
        {{ task.task }}<sub v-if="task.priorityHigh">with high priority</sub>
      </div>
      <img
        alt="delete logo"
        src="../assets/delete.png"
        @click="deleteTask(index)"
        style="flex-grow: 0"
      />
    </li>
  </ul>
</template>

<style scoped>
img {
  width: 25px;
  height: 25px;
  padding: 0px 40px;
  /* padding: 0 10px; */
}

img:hover {
  transform: scaleY(1.5);
  /* cursor: pointer; */
}
ul li {
  cursor: pointer;
  position: relative;
  padding: 12px 8px 12px 40px;
  background: #eee;
  font-size: 18px;
  transition: 0.2s;

  /* make the list items unselectable */
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;

  display: flex;
  flex-direction: row;
  justify-content: space-between;
}

/* Set all odd list items to a different color (zebra-stripes) */
ul li:nth-child(odd) {
  background: #f9f9f9;
}

/* Darker background-color on hover */
ul li:hover {
  /* transform: scaleX(1.15); */
  background: #ddd;
}

/* When clicked on, add a background color and strike out text */
/* ul li div.checked {
  background: greenyellow;
  color: red;
  text-decoration: line-through;
} */

.checked {
  background: #41b883;
  color: red;
  text-decoration: line-through;
}

/* Add a "checked" mark when clicked on */
/* ul li div.checked::before {
  content: "";
  position: absolute;
  border-color: green;
  border-style: solid;
  border-width: 0 2px 2px 0;
  top: 10px;
  left: 16px;
  transform: rotate(45deg);
  height: 15px;
  width: 7px;
} */

.checked::before {
  content: "";
  position: absolute;
  border-color: green;
  border-style: solid;
  border-width: 0 5px 5px 0;
  top: 10px;
  left: 16px;
  transform: rotate(45deg);
  height: 15px;
  width: 7px;
}

.priorityHigh {
  color: #000;
  /* background-color: #427aa1; */
}

.priorityMedium {
  color: #000;
  /* background-color: #397367; */
}

.priorityLow {
  color: #000;
  /* background-color: #68b3c8; */
}

/* Style the close button */
/* .close {
  position: absolute;
  right: 0;
  top: 0;
  padding: 12px 16px 12px 16px;
}

.close:hover {
  background-color: #f44336;
  color: white;
} */
</style>

<script>
export default {
  name: "TaskList",
  props: ["getTask"],
  data() {
    return {
      isTextStrike: false,
      taskList: [],
    };
  },
  methods: {
    strikeText(index) {
      [this.taskList] = [this.getTask];
      console.log("before taskList in tasklist:", this.taskList);

      this.taskList[index].doneTask = !this.taskList[index].doneTask;
      console.log("After taskList in tasklist:", this.taskList);
    },
    deleteTask(taskIndex) {
      [this.taskList] = [this.getTask];

      this.taskList.splice(taskIndex, 1);
    },
  },

  computed: {
    reversedTasks() {
      return [...this.getTask].reverse();
    },

    characterCount() {
      return this.getTask.length;
    },
  },
};
</script>
