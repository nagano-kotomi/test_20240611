<template>
  <div class="container">
    <!-- //validationErrorの値がtureの時だけ表示 -->
    <div v-if="validationError">タイトルを入力してください</div>
    <div v-if="apiError">サーバーでエラーが発生しました</div>
    <div class="item">
      <input type="text" name="title" placeholder="タイトル" v-model="inputTitle" />
    </div>
    <div class="item">
      <input type="text" name="period" placeholder="詳細" v-model="inputPeriod" />
    </div>
    <div class="item">
      <textarea
        name="detail"
        placeholder="完了期間"
        id
        cols="30"
        rows="10"
        v-model="inputDetail"
      ></textarea>
    </div>
    <div class="item">
      <button v-on:click="createTask">作成</button>
    </div>
  </div>
</template>

<script>
import api from '@/api'
export default {
  data() {
    return {
      inputTitle: '',
      inputPeriod: '',
      inputDetail: '',
      validationError: false, //条件判別
      apiError: false
    }
  },
  methods: {
    async createTask() {
      if (this.inputTitle === '') {
        this.validationError = true //未入力の場合ture
        return
      } else {
        this.validationError = false //入力したらfalse
      }
      let result
      try {
        //APIリクエスト
        result = await api.post('/tasks', {
          title: this.inputTitle,
          period: this.inputPeriod,
          detail: this.inputDetail
        })
      } catch (err) {
        this.apiError = true
        return
      }
      this.apiError = false
    }
  },
  onUpdate() {
    this.$emit('fetchTasks')
  }
}
</script>
