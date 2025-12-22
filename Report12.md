# 第12回 Webエンジニアリング演習 レポート
## 学籍番号（名前は書かなくてよい）
4723113
## 本日の感想
親からv-modelで渡されたデータが入ること- v-modelでモデルを指定してデータを渡すが分かった。
## 実装したコード
### AddTodo.vue
<script setup>
import {ref} from 'vue'
const todos = defineModel("todos")

const newTitle = ref('');
const nextId = ref(Math.max(0, ...todos.value.map((t) => t.id)) + 1);
function addTodo() {
  const title = newTitle.value;
  todos.value.push({ id: nextId.value++, title, completed: false });
  newTitle.value = '';
}
</script>

<template>
  <div id="app">
    <section>
      <h2>New Todo</h2>
      <div style="display: flex; align-items: center; gap: 0.5rem; margin: 0.25rem 0;">
        <input
          v-model="newTitle"
          placeholder="New todo title"
          aria-label="New todo title"
        />
        <button v-on:click="addTodo">Add</button>
      </div>
    </section>
  </div>
</template>>

### App.vue
<script setup lang=ts>
import AddTodo from './components/AddTodo.vue'
import { ref, computed } from 'vue';
const name = ref('Vue 3 with TypeScript');
type Todo = { id: number; title: string; completed: boolean};
const todos = ref<Todo[]>([
  { id: 1, title: 'Buy groceries', completed: false},
  { id: 2, title: 'Write report', completed: true},
  { id: 3, title: 'Call Alice', completed: false},
]);
const completedCount = computed(() => {
    return todos.value.filter(todo => !todo.completed).length;
});


</script>

<template>
  <div id="app">

    <section class="todo-app">
      <h2>Todos({{ completedCount }})</h2>

      <ul>
        <li
          v-for="todo in todos"
          :key="todo.id"
          style="display:flex; align-items:center; gap:0.5rem; margin:0.25rem 0;"
        >
          <input type="checkbox" v-model="todo.completed" />
          <span :style="{ textDecoration: todo.completed ? 'line-through' : 'none' }">
            {{ todo.title }}
          </span>
        </li>
      </ul>
    </section>
    
  </div>
  <div>
    <AddTodo v-model:todos="todos"/>
  </div>
</template>