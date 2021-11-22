<template>
    <div class="overlay">
        <todo-add
            @addTodo="addTodo"
            @showModal="showModal" 
        />
    </div>
</template>
<script>
import TodoAdd from '../TodoAdd.vue'
export default {
    components: { TodoAdd },
    methods: {  
        addTodo(title){
            this.$emit('addTodo', title)
        },
        showModal(){
            this.$emit('showModal')
        }
    }
}
</script> 

<style >
    .overlay{
        height: 100%;
        width: 100%;
        background: rgb(0, 0, 0, .5);
        position: absolute;
        top:0;
        left:0;
        bottom: 0;
        right: 0;
    }

</style>