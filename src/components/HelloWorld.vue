<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <hr/>
    <input type="text" placeholder="Enter Next Task" v-model="currentText" @keypress.enter="addTask"/>

    <transition-group
      name="flip-list"
      tag="ul"
    >
      <li
        v-for="(task, index) in toDoTasks"
        :key="task"
        @click="removeTask(index)"
        class="todo-tasks"
      >
        <span>{{ task }} </span>
      </li>

      <li
        v-for="(task, index) in doneTasks"
        :key="task"
        @click="restoreTask(index)"
        class="done-tasks"
      > 
        <span>{{ task }} </span>
      </li>
    </transition-group>
    <!-- <h3 v-if="toDoTasks.length === 0"> You don't have any pending tasks. </h3> -->

  </div>
</template>

<script>

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      currentText: '',
      toDoTasks: ["1", "2", "3", "4"],
      doneTasks: []
    }
  },
  methods: {
    addTask() {
      this.toDoTasks.push(this.currentText);
      this.currentText = '';
    },
    removeTask(taskIndex) {
      const removedTask = this.toDoTasks[taskIndex];
      this.toDoTasks = [
        ...this.toDoTasks.slice(0, taskIndex),
        ...this.toDoTasks.slice(taskIndex + 1)
      ];
      this.doneTasks.push(removedTask);
    },

    restoreTask(taskIndex) {
      const restoredTask = this.doneTasks[taskIndex];
      this.doneTasks = [
        ...this.doneTasks.slice(0, taskIndex),
        ...this.doneTasks.slice(taskIndex + 1)
      ];
      this.toDoTasks.push(restoredTask);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.flip-list-move {
  transition: transform 0.8s ease;
}

.hello {
  width: 50%;
  margin: auto;
  border: 1px solid lightgray;
  border-radius: 10px;
  box-shadow: 0px 0px 7px 0px #c7c7c7;
  background: #fff;
  margin-top: 50px;
}

input {
  font-size: 24px;
  padding: 10px 20px;
  width: 100%;
  border: none;
  background: inherit;
  border-bottom: 2px solid #eee;
}
input:focus, input:active, input:focus-visible {
  outline: none;
}

.done-tasks span {
  color: #d9d9d9;
  text-decoration: line-through;
}

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
  display: flex;
  flex-direction: column;
  margin: 0px;
}
li {
  display: inline-block;
  padding: 10px;
  width: 100%;
  border-bottom: 1px solid #eee;
  font-size: 24px;
  text-align: left;
  padding-left: 20px;
}

hr {
  border: 1px solid #c7c7c7;
  margin: 20px auto;
}

a {
  color: #42b983;
}

</style>
