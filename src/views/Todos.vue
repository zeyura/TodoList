<template>
    <div>

        <h2>Todo Application</h2>

        <add-todo
                @add-todo="addTodo"
        />

        <select v-model="todoFilter">
            <option value="all">All</option>
            <option value="not-completed">Not Completed</option>
            <option value="completed">Completed</option>
        </select>

        <hr>

        <router-link to="/">Home</router-link>

        <loader v-if="loading"></loader>
        <todo-list
                v-else-if="filteredTodos.length"
                :todos="filteredTodos"
                @remove-todo="removeTodo"
        />
        <p v-else>No Items!!!</p>

    </div>
</template>

<script>
    import TodoList from '@/components/TodoList'
    import AddTodo from '@/components/AddTodo'
    import Loader from '@/components/Loader'

    export default {
        name: 'App',
        components: {
            TodoList, AddTodo, Loader
        },
        data() {
            return {
                todos: [],
                loading: true,
                todoFilter: 'all'
            }
        },
        watch: {
            todoFilter(v) { // funcName == переменной для которой  делаем  наблюдение
               // console.log( v )
            }
        },
        mounted() {
            fetch('https://jsonplaceholder.typicode.com/todos?_limit=5')
                .then(res => res.json())
                .then(json => {
                    setTimeout(() => {
                        this.todos = json;
                        this.loading = false;
                    },500);
                });
        },
        computed: {
          filteredTodos() {
              if( this.todoFilter === 'all' ) return this.todos;
              else if( this.todoFilter === 'completed' ) return this.todos.filter( v => v.completed );
              else if( this.todoFilter === 'not-completed' ) return this.todos.filter( v => !v.completed );
          }
        },
        methods: {
            removeTodo(id) {
                this.todos = this.todos.filter( t => id !== t.id );
            },
            addTodo(o) {
                this.todos.push(o);
            }
        }
    }
</script>

<style scoped>

    select {
        margin: 20px auto;
        min-width: 20px;
        padding: 5px 10px;
    }

</style>