<script setup lang="ts">
import {ref} from "vue"

type Done = 'Finished' | 'not Finished'

interface Todo {
    name: string;
    isFinished: Done;
}


const todos = ref<Todo[]> ([
    { name: "vueを学ぶ", isFinished: 'not Finished' },
    { name: "1Q期末試験", isFinished: 'Finished' },
])

const newTodo = ref("")
const isFinishedTodo = ref<Done>('not Finished')

const addTodo = () => {
    if (newTodo.value !== "" ) {
        todos.value.push({ name: newTodo.value, isFinished: isFinishedTodo.value })
        newTodo.value = ""
    }
}

const turnTodo = (s:number) => {
    todos.value[s].isFinished='Finished'
}   

</script>

<template>
    <div>
        <h2>Todo List</h2>
        <ul>
            <li v-for="(todo,id) in todos" :key="todo.name" :class="{True: todo.isFinished=='Finished' ,False: todo.isFinished=='not Finished'}">
                <div>・{{ todo.name }} /{{ todo.isFinished }}
                <button v-if="todo.isFinished=='not Finished'" @click="turnTodo(id)">Done</button></div>
            </li>
        </ul> 
        <div>
        <label>
            タスク:
            <input v-model="newTodo" type="text" />
        </label>
        <button @click="addTodo">追加</button>
    </div>           
    </div>
</template>

<style>
.True{
    color: green;
}
.False{
    color: red;
}</style>
