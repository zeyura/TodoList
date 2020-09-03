<template>
    <div>
        <ul>
            <TodoItem
                v-for="(todo, i) in todos"
                :todoObj="todo"
                :index="i"
                @remove-todo="removeTodo"
            />
        </ul>
    </div>
</template>

<script>
    import TodoItem from '@/components/TodoItem'
    export default {
        name: "todo-list",
        props: [
            'todos'
        ],
        components: {
            TodoItem
        },
        methods: {
            removeTodo(id) {
                this.$emit('remove-todo', id);
            }
        }
    }
</script>

<style scoped lang="scss">

    ul {
        list-style: none;
        margin: 0;
        padding: 0;
        text-align: left;
    }

</style>