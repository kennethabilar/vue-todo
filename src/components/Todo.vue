<template>
    <div class="todo" v-bind:class="{ 'is-completed' : todo.completed }">
        <input type="checkbox" v-on:change="updateTodo" :checked="todo.completed">
        {{ todo.title }}
        <button class="del-btn" @click="$emit('del-todo', todo.id)">X</button>
    </div>
</template>

<script>
export default {
    name: 'Todo',
    props: ['todo'],
    methods: {
        updateTodo() {
            this.todo.completed = ! this.todo.completed
        }
    }
}
</script>

<style scoped>
    .todo {
        padding: 6px 10px;
        border-bottom: 1px solid #efefef;
    }

    .is-completed {
        text-decoration: line-through;
    }

    .del-btn {
        background-color: red;
        padding: 4px 8px;
        border: 0;
        border-radius: 50%;
        float: right;
        cursor: pointer;
    }
</style>