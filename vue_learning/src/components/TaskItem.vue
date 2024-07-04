<template>
  <div>
    <div v-if="loading">Loading...</div>
    <div v-else>
      <div v-if="error">エラーが発生しました。</div>
      <div v-else>
        <div class="task" v-for="task in tasks" :key="task.id">
          <!-- <div>id：{{ task.id }}</div> -->
          <div>タイトル：{{ task.title }}</div>
          <div>詳細　　：{{ task.detail }}</div>
          <div>完了期間：{{ task.period }}</div>
          <div class="deleteright">
            <button id="deletebutton" @click="deleteTask(task)">削除</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'
import api from '@/api'

export default {
  data() {
    return {
      tasks: [],
      loading: true,
      error: null
    }
  },
  mounted() {
    this.fetchTasks()
  },
  methods: {
    async fetchTasks() {
      try {
        const response = await api.get('/tasks')
        this.tasks = response.data
      } catch (err) {
        console.error('データの取得に失敗しました:', err)
        this.error = 'データの取得に失敗しました。'
      } finally {
        this.loading = false
      }
    },
    async deleteTask(task) {
      console.log('deleteTask', task.id)
     try {
       await api.delete(`/tasks/${task.id}`)
        // 削除後にタスクを再読み込みする
        await this.fetchTasks()
      } catch (err) {
        console.error('タスクの削除に失敗しました:', err.message)
      }
   }
    
  }
}
</script>

<style>
.task {
  display: block;
  border: 2px double cadetblue;
  margin-bottom: 5px;
  margin-right: 5px;
  padding: 10px;
  padding-right: 50px;
}
.deleteright{
  text-align: right;
}

#deletebutton{
  display: inline-block;
  text-decoration: none;
  background: #5a9c9c;/*ボタン色*/
  color: #FFF;
  border-bottom: solid 4px #627295;
  border-radius: 3px;
  margin-right: 0;
  margin-left: auto;
}
</style>
