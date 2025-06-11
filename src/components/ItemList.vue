<script setup lang="ts">
import { ref } from 'vue'

interface Item {
  name: string
  price: number
}

const items = ref<Item[]>([
  { name: 'たまご', price: 100 },
  { name: 'りんご', price: 160 }
])
const newItemName = ref('')
const newItemPrice = ref(0)

const addItem = () => {
    if (newItemName.value != "" && newItemPrice.value != 0) {
        items.value.push({ name: newItemName.value, price: newItemPrice.value })
        newItemName.value = ""
        newItemPrice.value = 0
    }
}

interface Todo {
  name: string
  isDone: boolean
}
const todos = ref<Todo[]>([
    { name: 'デーサイ', isDone: false}
])
const newTodoName = ref('')
const addTodo = () => {
    if (newTodoName.value != "" ) {
        todos.value.push({ name: newTodoName.value, isDone: false })
        newTodoName.value = ""
    }
}

const doneTodo = (todo: Todo) => {
    todo.isDone = true
}
</script>

<template>
  <div>
    <div>ItemList</div>
    <ul>
      <li v-for="item in items" :key="item.name" :class="{ over500: item.price >= 500 }">
        <div>名前: {{ item.name }}</div>
        <div>{{ item.price }} 円</div>
        <div v-if="item.price >= 10000">高額商品</div>
      </li>
    </ul>
    <div>
      <label>
        名前
        <input v-model="newItemName" type="text" />
      </label>
      <label>
        価格
        <input v-model="newItemPrice" type="number" />
      </label>
      <button @click="addItem">add</button>
    </div>
  </div>
  <div>
    <div>TodoList</div>
    <div>未完</div>
    <ul>
      <div v-for="todo in todos" :key="todo.name" >
        <li v-if="!todo.isDone"> {{ todo.name }}
            <button @click="doneTodo(todo)">✔️</button>
        </li>
    </div>
    </ul>
    <div>完了</div>
    <ul>
      <div v-for="todo in todos" :key="todo.name" >
        <li v-if="todo.isDone"> {{ todo.name }}</li>
      </div>
    </ul>
    <div>
      <label>
        名前
        <input v-model="newTodoName" type="text" />
      </label>
      <button @click="addTodo">add</button>
    </div>
  </div>
</template>

<style>
.over500 {
  color: red;
}
</style>