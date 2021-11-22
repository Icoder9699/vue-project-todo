<template >
    <li >
        <p :class="{completed: todo.completed}">
            <input 
                type="checkbox" 
                style="margin-right: 10px;"
                :checked="todo.completed"
                @change="$emit('completeTodo', todo.id)"
            >
            <strong>{{index + 1}}.&nbsp;</strong>{{todo.title}} 
        </p> 
        <button 
            @click="$emit('removeTodo', todo.id)"
        >
            &times;
        </button>
    </li>
</template>
<script>
export default {
    props: {
        todo: {
            type: Object,
            required: true
        },
        index: Number,
    },
}
</script>
<style scoped>
    li{
        display: flex;
        justify-content: space-between;
        align-items: center;
        border: 1px solid #ccc;
        margin: 5px 0;
        padding: 10px;
        border-radius: 5px;
    }
    button{
        border: 1px solid red;
        cursor: pointer;
        color: red;
        background: transparent;
        font-weight: bold;
        border-radius: 5px;
    }
    button:hover{
        background: red;
        color: #fff;
    }

    .completed{
        text-decoration: line-through;
    }
</style>