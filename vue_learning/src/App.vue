<template>
  <div id="app">
    <Header/>
    <Form/>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Form from './components/Form.vue'

export default {
  name: 'app',
  components: {
    Header,Form
  }
}

</script>

<style lang="css">
</style>