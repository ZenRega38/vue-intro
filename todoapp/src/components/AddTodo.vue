<template>
    <div>
        <div class="container">
            <br><br>
            <h1 class="text-center">Todos App</h1>
            <form @submit="addTodo">
                <div class="form-group">
                    <input type="text" v-model="title" placeholder="title"  name="title" id="" class="form-control"/>
                </div>
                <div class="form-group">
                    <button class="btnAdd btn-block">
                        Add Todo
                    </button>
                </div>
            </form>
        </div>
    </div>
</template>

<script>
export default {
    name: "AddTodo",
    data(){
        return{
            title:''
        }
    },
    methods:{
        addTodo(e){
            e.preventDefault()

            const newTodo = {
                id:Date.now(),
                title:this.title,
                completed:false
            }

            this.$emit("add-todo",newTodo)

            this.title = '';
        }
    }
};
</script>

<style scoped>

    .btnAdd {
        border: none;
        background-color: rgb(0, 102, 255);
        color: white;
        padding: 12px;
        border-radius: 10px;
    }
</style>