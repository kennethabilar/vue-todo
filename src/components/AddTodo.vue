<template>
    <div>
        <h2>Add Todo</h2>
        <form v-on:submit="addTodo">
            <label for="title">Title</label>
            {{ ' ' }}
            <input type="text" name="title" v-model="title">
            {{ ' ' }}
            <input type="submit" value="Add">
        </form>
    </div>
</template>

<script>
export default {
    name: 'AddTodo',
    data() {
        return {
            title: ''
        }
    },
    methods: {
        addTodo(e) {
            e.preventDefault();
            
            const newTodo = {
                title: this.title,
                completed: false
            }

            this.$emit('add-todo', newTodo)
            this.title = ''
        }
    }
}
</script>