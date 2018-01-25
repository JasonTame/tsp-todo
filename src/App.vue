<template>
<div id="app">
  <h1 class="text-center title">Simple Task Manager</h1>


  <div class="row">
    <div class="taskList col-xs-12">

      <div class="taskButton">

        <input id="addTaskInput" value="Add task name here" v-model="addTask" /> <button class="btn btn-info" @click="addNewTask">Add Task</button>

      </div>
      <br>
      <ul>
        <li v-for="(task, key) in tasks"><input type="checkbox" v-model="task.completed" /> {{task.description}}
          <button class="btn btn-danger" @click="deleteTask(key)"><i class="fa fa-trash" aria-hidden="true"></i></button> </li>
      </ul>


    </div>

  </div>

  <div class="row">
    <div class="col-xs-6 taskList">
      <h4>Incomplete tasks </h4>
      <ol>
        <li v-for="task in incompleteTasks" v-text="task.description"></li>
      </ol>
    </div>
    <div class="col-xs-6 taskList">
      <h4>Complete tasks </h4>
      <ol>
        <li v-for="task in completeTasks" v-text="task.description"></li>
      </ol>
    </div>
  </div>
  </ul>
</div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      addTask: "",
      tasks: [{
          description: "Take out trash",
          completed: true
        },
        {
          description: "Do washing",
          completed: false
        },
        {
          description: "Iron clothes",
          completed: true
        },
        {
          description: "Grocery shopping",
          completed: false
        }
      ]
    }
  },
  computed: {
    incompleteTasks() {
      return this.tasks.filter(task => !task.completed);
    },

    completeTasks() {
      return this.tasks.filter(task => task.completed);
    }
  },
  methods: {
    addNewTask() {
      this.tasks.push({
        description: this.addTask,
        completed: false
      });

      this.addTask = "";
    },

    deleteTask(key) {
      this.tasks.splice(this.tasks.indexOf(key), 1);
    }
  }
}
</script>

<style>
body {
  margin: 0 auto;
  width: 100%;
  background-color: #0f0c0e;
}

.title {
  padding-top: 20px;
}

h1,
h2,
h3,
h4 {
  color: #f7ab1d;
}

p,
li {
  color: #fff;
}



ul {
  list-style: none;
  padding: 0px 10px 0px 10px
}

li {
  position: relative;
  padding: 10px 0px 10px 0px;
}

li>button {
  position: absolute;
  right: 0;
}

.taskButton {
  margin: 0 auto;
  text-align: center;
  padding: 10px;
}

.taskButton button {}

button:hover {
  cursor: pointer;
}

.taskButton {
  margin: 0 auto;
}

.taskList {
  margin: 0 auto;
  padding: 10px;
}
</style>
