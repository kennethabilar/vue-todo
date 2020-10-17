<template>
    <div class="home">
        <AddTodo v-on:add-todo="addTodo" />
        <Todos v-on:del-todo="delTodo" v-bind:todos="todos" />
    </div>
</template>

<script>
// @ is an alias to /src
import Todos from '@/components/Todos.vue'
import AddTodo from '@/components/AddTodo.vue'
import axios from 'axios'
import { v4 as uuidv4 } from 'uuid'

export default {
    name: 'Home',
    components: {
        AddTodo,
        Todos
    },
    data() {
        return {
            todos: []
        }
    },
    methods: {
        addTodo(newTodo) {
            const { title, completed } = newTodo

            axios.post('https://jsonplaceholder.typicode.com/todos', { title, completed })
                .then(res => {
                    if(res.status === 201) {
                        res.data.id = uuidv4()
                        this.todos = [...this.todos, res.data]
                    }
                })
                .catch(err => console.log(err))
        },
        delTodo(id) {
            axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
                .then(res => {
                    if(res.status === 200) {
                        this.todos = this.todos.filter(todo => todo.id !== id)
                    }
                })
                .catch(err => console.log(err))
        }
    },
    created() {
        axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
            .then(res => this.todos = res.data)
            .catch(err => console.log(err))
    }
}
</script>
