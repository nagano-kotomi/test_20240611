<template>
  <div class="container">
    <!-- //validationErrorの値がtureの時だけ表示 -->
    <div v-if="validationError">タイトルを入力してください</div>
    <div v-if="apiError">サーバーでエラーが発生しました</div>
    <div class="item">
      <div class="text" style="width:210px; height:20px">
        タスク入力
      </div>
      <textarea type="text" name="title" placeholder="タイトル" style="width:210px; height:50px" v-model="inputTitle" ></textarea>
    </div>
    <div class="item">
      <textarea type="text" name="detail" placeholder="詳細" style="width:210px; height:50px" v-model="inputDetail"></textarea>
    </div>
    <div class="item">
      完了期間
      <input
        name="period"
        id
        type="datetime-local"
        v-model="inputPeriod"
      ></input>
    </div>
    <div class="right">
      <button class="button" v-on:click="createTask">作成</button>
    </div>
  </div>
</template>

<script>
import api from '@/api'
export default {
  data() {
    return {
      inputTitle: '',
      inputDetail: '',
      inputPeriod: '',
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
          detail: this.inputDetail,
          period: this.inputPeriod,
        })
        await api.get('/tasks')
        this.$emit('task-created')
        this.inputTitle = ''
        this.inputDetail = ''
        this.inputPeriod = ''
      } catch (err) {
        this.apiError = true
        console.error('API リクエストでエラーが発生しました:', err.message)
        return
      }
      this.apiError = false
    },
  },
  onUpdate() {
    this.$emit('fetchTasks')
  }
}
</script>

<style>
.item{
  margin-bottom: 5px;
}

.button{
  display: inline-block;
  text-decoration: none;
  background: #5a9c9c;/*ボタン色*/
  color: #FFF;
  border-bottom: solid 4px #627295;
  border-radius: 3px;
  }
.text{
  text-align: center;
  color: rgb(42, 106, 235);
  border: 2px double cadetblue;
  margin-bottom: 10px;
}
.right{
  padding-left: 172px;
}
</style>
