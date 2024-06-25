<template>
  <div id="app">
    <div><Header /></div>
    <div id="item">
      <div class="form"><Form /></div>
      <div class="task-item"><TaskItem /></div>
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
  }
}
</script>

<style>
body {
  font-family: Arial, sans-serif;
}

#item {
  display: flex;
}
.form {
  margin: 20px;
}
.task-item {
  margin: 20px;
}
</style>
