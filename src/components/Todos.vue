<template>
    <div>
        <h2>Todos</h2>
        <div v-bind:key="todo.id" v-for="todo in todos">
            <Todo v-on:del-todo="$emit('del-todo', todo.id)" v-bind:todo="todo" />
        </div>
    </div>
</template>

<script>
import Todo from '@/components/Todo.vue'

export default {
    name: 'Todos',
    components: {
        Todo
    },
    props: ['todos']
}
</script>
