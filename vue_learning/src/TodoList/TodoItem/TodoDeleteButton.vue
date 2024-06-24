<template>
    <button @click="deleteTodo">Delete</button>
  </template>
  
  <script>
  export default {
    name: 'TodoDeleteButton',
    methods: {
      deleteTodo() {
        this.$emit('delete')
      }
    }
  }
  </script>
  
  <style scoped>
  /* 任意のスタイルを追加 */
  </style>
  