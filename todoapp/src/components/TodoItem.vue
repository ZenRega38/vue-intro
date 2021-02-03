<template>
    <div class="container">
        <div class="todo-item" v-bind:class="{'is-complete':todo.completed}">
            <p>
                <input type="checkbox" v-on:change="markComplete" v-bind:checked="todo.completed">
                {{ todo.title }}
                <button @click="update" class="update">Update</button>
                <button @click="$emit('delete-todo',todo.id)" class="del">x</button>
            </p>
        </div>
        <div v-if="this.flag">
            <form @submit="updateTodo">
                <div class="form-group">
                    <input type="text" v-model="updatedTitle" placeholder="title" required class="form-control">
                </div>
                <div class="form-group">
                    <button class="btn">Submit</button>
                </div>
            </form>
        </div>
    </div>
</template>

<script>
export default {
    name:"TodoItem",
    props:['todo','todos'],
    methods:{
        markComplete() {
            this.todo.completed = !this.todo.completed;
        },
        update(){
            this.flag = !this.flag
        },
        updateTodo(e){
            e.preventDefault()

            this.todos.filter((todo) => {
                if(todo.id == this.todo.id){
                    todo.title = this.updatedTitle
                }
            })

            this.flag = false
        }
    },
    data(){
        return {
            flag:false,
            updatedTitle:''
        }
    }
}
</script>

<style scoped>
    .todo-item {
        background: #f4f4f4;
        padding: 10px;
        margin:20px;
        border-bottom: 1px #ccc dotted;
    }

    .is-complete {
        text-decoration: line-through;
    }

    .del {
        background: #ff0000;
        color: #fff;
        border: none;
        padding: 4px 10px;
        border-radius: 3px;
        cursor: pointer;
        float: right;
    }

    .update {
        float: right;
        margin-left: 8px;
        text-decoration: none;
        border: none;
        background: orange;
        color: white;
        padding: 4px 8px;
        border-radius: 3px;
    }

    .btn {
        border: none;
        background-color: rgb(0, 102, 255);
        color: white;
        size: 11px;
        padding: 4px 6px;
        border-radius: 3px;
    }
</style>