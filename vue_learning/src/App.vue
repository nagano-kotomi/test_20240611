<template>
  <div id="app">
    <div><Header /></div>
    <div id="item">
      <div class="form"><Form @task-created="refreshTasks"/></div>
      <div class="task-item"><TaskItem ref="taskItem"/></div>
    </div>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Form from './components/Form.vue'
import TaskItem from './components/TaskItem.vue'

export default {
  name: 'app',
  components: {
    Header,
    Form,
    TaskItem
  },
  methods: {
    refreshTasks() {
      this.$refs.taskItem.fetchTasks()
      this.$refs.taskItem.sortTasksByDetailDate()
    }
  }
}
</script>

<style>
body {
  font-family: Arial, sans-serif;
}

#item {
  display: flex;
  flex-direction: row;
}
.form {
  margin: 20px;
}
.task-item {
  margin: 20px;
}

@media (max-width: 600px){
  #item{
    flex-direction: column;
  }
  .form{
    margin: 20px auto;
  }
  .task-item {
    margin: 20px;
  }
}
</style>
