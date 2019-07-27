<template>
    <div>
        <div v-bind:key="todo.id" v-for="todo in todos">
            <TodoItem v-bind:todo="todo" v-on:delete-todo="$emit('delete-todo', todo.id)"/>
        </div>
    </div>
</template>
<script>
import TodoItem from './TodoItem.vue' 
export default {
    name:'Todos',
    components:{
        TodoItem
    },
    props:[
        'todos'
    ],
    data(){
        return {
            
        }
    }
}
</script>
<style>

</style>

