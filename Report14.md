# 第14回 Webエンジニアリング演習 レポート
## 学籍番号
4723113
## 実装した内容

## src/views/About.vue
<script setup lang="ts">
</script>
<template>

<h2>About</h2>
<p>todoリスト</p>
</template>

## src/views/TodoDetail.vue
<script setup lang="ts">
    import { computed } from 'vue'
    import {useRoute} from 'vue-router'
    import {useTodosStore} from '../stores/todoStore'
    const todoStore = useTodosStore()
    const route = useRoute()
    const id = Number(route.params.id)
    const todo = computed(() =>
    todoStore.todos.find(t => t.id === id)
    )
</script>

<template>
  <div v-if="todo">
    <h1>Todo Detail</h1>

    <p><strong>Title:</strong> {{ todo.title }}</p>
    <p><strong>Description:</strong> {{ todo.description }}</p>
    <p>
      <strong>Completed:</strong>
      {{ todo.completed ? '完了' : '未完了' }}
    </p>
  </div>
  <div v-else>
    <p>指定されたTODOは存在しません。</p>
  </div>
</template>