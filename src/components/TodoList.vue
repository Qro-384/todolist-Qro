<script setup lang="ts">
import {ref} from "vue"

type Done = 'default' | 'Finished' | 'not Finished'

interface Todo {
    name: string;
    isFinished: Done;
}


const todos = ref<Todo[]> ([
    { name: "vueを学ぶ", isFinished: 'not Finished' },
    { name: "1Q期末試験", isFinished: 'Finished' },
    { name: "Dynamixのスタミナを消費する", isFinished: 'not Finished' },
])

const newTodo = ref("")
const isFinishedTodo = ref<Done>('default')

const addTodo = () => {
    if (newTodo.value !== "" && isFinishedTodo.value!== 'default') {
        todos.value.push({ name: newTodo.value, isFinished: isFinishedTodo.value })
        newTodo.value = ""
        isFinishedTodo.value = 'default'
    }
}

const turnTodo = (s:string) => {
    if (s!== 'not Finished') {
        s = 'Finished'
    }
}   

</script>

<template>
    <div>
        <h2>Todo List</h2>
        <ul>
            <li v-for="todo in todos" :key="todo.name" :class="{True: todo.isFinished=='Finished' ,False: todo.isFinished=='not Finished'}">
                <div>・{{ todo.name }} /{{ todo.isFinished }}
                <button v-if="todo.isFinished=='not Finished'" @click="turnTodo(todo.isFinished)">Done !!</button></div>
                    
            </li>
        </ul>            
    </div>
</template>

<style>
.True{
    color: green;
}
.False{
    color: red;
}</style>
