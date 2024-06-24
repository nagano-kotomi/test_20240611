<template>
    <div class="container">
      <div class="item">
        <input type="text" name="title" placeholder="タイトル" v-model="inputTitle">
      </div>
      <div class="item">
        <input type="text" name="period" placeholder="詳細" v-model="inputPeriod">
      </div>
      <div class="item">
        完了期限
        <input type="date" name="detail" placeholder="完了期間" v-model="inputDetail"></input>
      </div>
      <div class="item">
        <button v-on:click="createTask">作成</button>
      </div>
    <div>
      <table border="1">
        <tr>{{ DisplayTitle }}</tr>
        <tr>{{ DisplayPeriod }}</tr>
        <tr>{{ DisplayDetail }}</tr>
    </table>
    </div>
    </div>
  </template>
  <!-- textare -->

<script>
export default {
  data() {
    return {
      inputTitle: "",
      inputPeriod: "",
      inputDetail: "",
      DisplayTitle: "",
      DisplayPeriod: "",
      DisplayDetail: ""
    }
  }
  ,methods: {
      createTask() {
          // タスクを作成する処理
        this.DisplayTitle = this.inputTitle
        this.DisplayPeriod = this.inputPeriod
        this.DisplayDetail = this.inputDetail
      }
  }
}
</script>