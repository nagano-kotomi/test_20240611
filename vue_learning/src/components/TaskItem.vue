<template>
    <div>
        <div v-if="loading">Loading...</div>
        <div v-else>
            <div v-if="error">エラーが発生しました。</div>
                <div v-else>
                    <button @click="deleteTask">削除</button>
                    <div v-for="task in tasks" :key="task.id">
                        <div>{{ task.title }}</div>
                        <div>{{ task.period }}</div>
                        <div>{{ task.detail }}</div>
                    </div>
                    
                </div>
        </div>
    
    </div>
</template>

<script>
import { ref } from 'vue';
import api from "@/api";

export default {
  data() {
    return {
      tasks: ref([]),
      loading: true,
      error: null
    };
  },
  mounted() {
    this.fetchTasks();
  },
  methods: {
    async fetchTasks() {
      try {
        const response = await api.get('/tasks');
        this.tasks = response.data;
      } catch (err) {
        console.error('データの取得に失敗しました:', err);
        this.error = 'データの取得に失敗しました。';
      } finally {
        this.loading = false;
      }
    },
    async deleteTask() {
      try {
        await api.delete(`/tasks`);
        // 削除後にタスクを再読み込みする
        await this.fetchTasks();
      } catch (err) {
        console.error('タスクの削除に失敗しました:', err);
      }
    }
  }
};
</script>