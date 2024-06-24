<template>
  <div id="app">
    <Header/>
    <Form/>
    <TaskItem/>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Form from './components/Form.vue'
import TaskItem from './components/TaskItem.vue'

export default {
  name: 'app',
  components: {
    Header,Form,
    TaskItem
  }
}

</script>

<style lang="css">
</style>