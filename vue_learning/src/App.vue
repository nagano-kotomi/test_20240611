<template>
  <div id="app">
    <div><Header/></div>
    <div class="left"><Form/></div>
    <div class="left"><TaskItem/></div>
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

<style>
body {
  font-family: Arial, sans-serif;
}

.left{
  float: left;
}
</style>