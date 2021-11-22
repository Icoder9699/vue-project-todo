<template>
    <form @submit.prevent="addTodo">
        <input 
            type="text" 
            placeholder="what we will do today ?" 
            v-model="title"
        />  
        <button class="btn btn-add">Add</button>
        <button class="btn btn-delete" @click="showModal">&times;</button>
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
                this.$emit('showModal')
            },
            showModal(){
                this.$emit('showModal')
            }
        }
    }
</script>

<style scoped>
    form{
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        width: 500px;
        background: #fff;
        padding: 20px;
        border-radius: 5px;
    }
    input {
        width: 80%;
        height: 50px;
        outline: none;
        padding: 5px;
        transition: all 300ms linear;
    }
    input:focus{
        border: 1px solid rgb(137, 125, 207);
    }
    .btn-add{
        width: 20%;
        height: 50px;
        border: 1px solid rgb(137, 125, 207);
        background: #fff;
        transition: all 300ms linear;
    }
    .btn-add:hover{
        background: rgb(137,125,207);
        color: #fff;
        cursor: pointer;
    }
    .btn-delete{
        position: absolute;
        top: -15px;
        background: transparent;
        border:1px solid red;
        color: red;
        height: 30px;
        width: 30px;
        border-radius: 50%;
        cursor: pointer;
        font-size: 16px;
    }
    .btn-delete:hover{
        background: red;
        color: #fff;
        cursor: pointer;
    }
</style>