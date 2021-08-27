<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <hr/>
    <input type="text" placeholder="Enter next task" v-model="currentText" @keypress.enter="addTask"/>

    <transition-group
      name="flip-list"
      tag="ul"
    >
      <li
        v-for="(task, index) in toDoTasks"
        :key="task"
        @click="finishTask(index)"
        class="todo-tasks"
        title="Finish task"
      >
        <span>{{ task }} </span>
        <span title="Remove task" @click.stop="deleteTask(index)" class="delete-task">&#10006;</span>
      </li>

      <li
        v-for="(task, index) in doneTasks"
        :key="task"
        @click="restoreTask(index)"
        class="done-tasks"
        title="Add the task back to todolist"
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
      toDoTasks: [],
      doneTasks: []
    }
  },
  methods: {
    addTask() {
      this.toDoTasks.push(this.currentText);
      this.currentText = '';
    },
    finishTask(taskIndex) {
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
    },
    deleteTask(taskIndex) {
      this.toDoTasks = [
        ...this.toDoTasks.slice(0, taskIndex),
        ...this.toDoTasks.slice(taskIndex + 1)
      ];
    }
  }
}
</script>


<style scoped>

.flip-list-move {
  transition: transform 0.5s ease;
}

.flip-list-enter-active,
.flip-list-leave-active {
  transition: all 0.5s ease;
}

.flip-list-enter-from,
.flip-list-leave-to {
  opacity: 0;
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

input::placeholder {
  color: #bdbdbd;
  font-style: italic;
}

input:focus, input:active, input:focus-visible {
  outline: none;
}

.delete-task {
  margin-left: auto;
  display: none;
  font-size: 20px;
  
}

li:hover .delete-task {
  display: inline;
}

.delete-task:hover {
  color: #d32f2f;
  transition: color .2s ease-in;
}

.done-tasks span {
  color: #d9d9d9;
  text-decoration: line-through;
}


h1 {
  background: #e0e0e0;
  margin: 0;
  padding: 20px;
  color: #4d4d4d;
}

ul {
  list-style-type: none;
  padding: 0;
  display: flex;
  flex-direction: column;
  margin: 0px;
}

li {
  color: #4d4d4d;
  width: 100%;
  border-bottom: 1px solid #eee;
  font-size: 24px;
  text-align: left;
  padding: 10px 20px;
  cursor: pointer;
  display: flex;
}

hr {
  border: 1px solid #c7c7c7;
  margin: 0px;
}

a {
  color: #42b983;
}

</style>
