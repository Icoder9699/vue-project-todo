<template>
    <form @submit.prevent="addTodo">
        <input 
            type="text" 
            placeholder="what we will do today ?" 
            v-model="title"
        />  
        <button class="btn btn-add">Add</button>
    </form>
</template>

<script>
    export default {
        data(){
            return{
                title: '',
                error: false
            }
        },
        methods: {
            addTodo(){
                if(this.title === ''){
                    return
                }
                const todo = {
                    id: Date.now(),
                    completed: false,
                    title: this.title
                };
                this.$emit('addTodo', todo)
                this.title = ''
            }
        }
    }
</script>

<style scoped>
    form{
        width: 100%;
        height: 50px;
        margin-bottom: 20px;
    }
    input {
        width: 80%;
        height: 100%;
        outline: none;
        padding: 5px;
        transition: all 300ms linear;
    }
    input:focus{
        border: 1px solid rgb(137, 125, 207);
    }
    button{
        width: 20%;
        height: 100%;
        border: 1px solid rgb(137, 125, 207);
        background: #fff;
        transition: all 300ms linear;
    }
    button:hover{
        background: rgb(137,125,207);
        color: #fff;
        cursor: pointer;
    }
</style>