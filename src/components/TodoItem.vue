<template>
    <li>
        <span :class="{done: todoObj.completed}">
            <input type="checkbox" @change="todoObj.completed = !todoObj.completed">
            <strong>{{index+1}}</strong>
            {{todoObj.title | toApper}}
        </span>
        <button class="rm"
            @click="$emit('remove-todo', todoObj.id)"
        >&times;</button>
    </li>
</template>

<script>
    export default {
        name: "todo-item",
        props: {
            todoObj: {
                type: Object,
                required: true
            },
            index: Number
        },
        filters: {
            toApper(v) {
                return v.toUpperCase()
            }
        }
    }
</script>

<style scoped lang="scss">
    li {
        border: 1px solid #444;
        display: flex;
        justify-content: space-between;
        padding: .75rem .5rem;
        margin: 1rem 0;
    }
    .rm {
        background-color: palevioletred;
        color: white;
        border-radius: 50%;
        border: none;
        cursor: pointer;
        opacity: .9;

        &:hover {
            opacity: 1;
        }
        &:focus {
            outline: deepskyblue 1px solid;
        }
    }
    .done {
        text-decoration: line-through;
    }
    input[type=checkbox] {
        margin-right: .6rem;
    }
</style>