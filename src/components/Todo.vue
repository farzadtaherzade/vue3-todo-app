<template>
<div class="container">
    <form class="form" @submit.prevent="addTodo">
        <h1>Todo App</h1>
        <input type="text" id="add-task" placeholder="What do you have planned for today?" v-model="text">
        <button><strong class="strong-todo">Add Todo</strong></button>
    <div class="todos">
        <h2 class="h2">Todo List</h2>
        <div class="todo" v-for="todo in todos" :key="todo">
            <h4  :class="{'check':check}">{{todo.task}}</h4>
            <div class="item">
                <span class="todo-button" @click="removeTodo(todo)"><fa icon="trash-alt" class="icon" /></span>
            </div>
        </div>
    </div>
    </form>
</div>
</template>

<script>
export default {
    data() {
        let todos = [

            ]
        
        if (localStorage.getItem('todos') == null) {
            localStorage.setItem('todos', JSON.stringify(todos))
        }

        todos = localStorage.getItem('todos')

        todos = JSON.parse(todos)
        return {
            todos :todos,
            text : '',

            // responsive
            check : false,
        }
    },
    methods: {
        addTodo() {
            if (this.text === '') {
                console.log('enter value')
            }else{
                this.todos.push({task:this.text})
                localStorage.setItem('todos',JSON.stringify(this.todos))
                this.text = ''
            }
        },
        removeTodo(todo) {
            let index = this.todos.findIndex(tasks => tasks.task == todo.task)
            this.todos.splice(index, 1)

            let newTodo = JSON.stringify(this.todos)
            localStorage.setItem('todos', newTodo)
        },
        handelView() {
            if (window.innerWidth <= 700) {
                this.mobileView = true
            }else{
                this.mobileView = false
            }
        },
        checks() {

        }
    },
    created() {
        this.handelView()
    },
}
</script>

<style>
*{
    margin: 0;
    padding: 0;
    color: #000;
    font-family: sans-serif;
}

body{
    background-color: #222222;
}

.container{
    margin-top:3.4rem ;
    margin-left:1rem ;
    margin-right:0rem ;

}

.form{
    max-width: 500px;
    width: 100%;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    text-align: center; 
}

.form > button, .strong-todo{
    padding: 0.7rem;
    border: none;
    background-color: #121212;
    font-size: 15px;
    color: #888;
    border-radius:5px;
    margin-right: 1rem;
    cursor: pointer;
}

#add-task {
    background-color: #121212;
    flex: 1 1 0%;
    padding: 1rem;
    border-radius:5px;
    margin-right: 1rem;
    border: none;
    margin-top: 10px;
    margin-bottom: 7px;
    color: #888;
}

.todos{
    margin-top: 10px;
}

.todo{
    display: flex;
    flex-direction: row;
    padding: 0.86rem;
    background-color: #4455;
    max-width: 460px;
    justify-content: space-between;
    margin-top: 10px;
    margin-bottom: 10px;
    font-size: 0.9em;

    border-radius: 0.6rem;
}
h4{
    color: #fff;
}

.todo-button, .s-todo{
    padding: 0.2rem;
    border: none;
    color: #999;
    border-radius:5px;
    cursor: pointer;
}

.icon{
    padding: 2px;
    color: #fff;
}

.check{
    -webkit-text-decoration-line: line-through; /* Safari */
   text-decoration-line: line-through; 
}

</style>