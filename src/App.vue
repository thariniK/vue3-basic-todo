<template>
<h1>Vue 3 To-Do App</h1>
<form @submit.prevent="addTodoList">
    <label>To Do</label>
    <input name="todo" v-model="addTodo">
    <button type="submit">Add To-Do</button>
</form>
<div style="margin-top: 20px;">
    <button @click="markAllDone()">Mark all as done</button>&nbsp;
    <button @click="removeAll()">Remove All</button>
</div>
<ul>
    <li v-for="(todo, index) in todoList" :key="todo.id">
        <span :class="{ done: todo.done }" @click="toggleTodo(todo)">{{ todo.content }}</span>&nbsp;
        <a @click.prevent="removeTodo(index)">remove</a>
    </li>
</ul>
</template>

<script>
import {
    ref
} from 'vue';

export default {
    setup() {
        const addTodo = ref('');
        const todoList = ref([]);

        function addTodoList() {
            todoList.value.push({
                id: todoList.value.length + 1,
                done: false,
                content: addTodo.value
            })
            addTodo.value = ''
        }

        function toggleTodo(todo) {
            todo.done = !todo.done
        }

        function removeTodo(index) {
            todoList.value.splice(index, 1);
        }

        function markAllDone() {
            todoList.value.forEach((todo) => todo.done = true)
        }

        function removeAll() {
            todoList.value = [];
        }

        return {
            addTodo,
            addTodoList,
            todoList,
            toggleTodo,
            removeTodo,
            markAllDone,
            removeAll
        };
    }
}
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    /*text-align: center;*/
    color: #2c3e50;
    margin-top: 60px;
}

a {
    cursor: pointer;
    color: mediumblue;
}

ul li span {
    cursor: pointer;
}

.done {
    text-decoration: line-through;
}
</style>
