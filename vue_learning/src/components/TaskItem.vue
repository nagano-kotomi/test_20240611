<template>
  <div>
    <div v-if="loading">Loading...</div>
    <div v-else>
      <div v-if="error">エラーが発生しました。</div>
      <div v-else>
        <div class="task" v-for="task in tasks" :key="task.id">
          <!-- <div>id：{{ task.id }}</div> -->
          <div>タイトル：{{ task.title }}</div>
          <div>詳細：{{ task.period }}</div>
          <div>完了期間：{{ task.detail }}</div>
          <div>
            <button @click="deleteTask(task)">削除</button>
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
      tasks: ref([]),
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
     console.log('deleteTask', task._id)
     try {
       await api.delete(`/tasks/${task._id}`)
       // 削除後にタスクを再読み込みする
       await this.fetchTasks()
     } catch (err) {
       console.error('タスクの削除に失敗しました:', err)
     }
   }
    
  }
}
</script>

<style>
.task {
  display: inline-block;
  border: 2px double #ccc;
  margin-bottom: 5px;
  margin-right: 5px;
  padding: 10px;
}
</style>
