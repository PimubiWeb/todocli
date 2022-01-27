<template>
  <div class="container">

      

       <input type="text" class="todo-input" placeholder="Enter a title todo"
       v-model="newTodo" @keyup.enter="addTodo">
       
        <input type="text" class="todo-input" placeholder="Enter a description todo"
       v-model="description" @keyup.enter="addTodo">

        <button @click="addTodo" class="todo-btn">Add</button>

        <transition-group name="fade" enter-active-class="animated fadeInUp" leave-active-class="animated fadeOutDown">
        
        <todoItem v-for="(todo,index) in todosFiltered" 
        :key="todo.id" :todo="todo" :index="index"
        @removedTodo="removeTodo" @changedStatus="changeStatus" :class="{status :todo.status}"
        @changedPriority="changePriority">
        <!--<div class="todo-item-left">
                <input type="checkbox" @click="changeStatus(index)">
                <div class="todo-item-label" :class="{status : todo.status}">
                   <div>{{todo.title}}</div>
                   <div>{{todo.description}}</div>
                   <div>{{todo.date}}</div>
                </div>
            </div>

            <div>
                <button @click="changePriority(index, prio =0)">High</button>
                <button @click="changePriority(index, prio =1)">Medium</button>
                <button @click="changePriority(index, prio =2)">Low</button>
            </div>
            <div class="remove-item" @click="removeTodo()">
                🗑️
            </div>
        </div> -->
        </todoItem>
        </transition-group>

        <div class="extra-container">
            <input type="text" placeholder="Search" v-model="text" @keyup.enter="search">

            <div>{{this.todos.length}} total {{ remaining }} todo left</div>
        </div>

        <div class="extra-container">
            <div>
                <button :class="{ active: filter == 'all' }" @click="filter = 'all'">All</button>
                <button :class="{ active: filter == 'active' }" @click="filter = 'active'">Active</button>
                <button :class="{ active: filter == 'completed' }" @click="filter = 'completed'">Completed</button>
            </div>

            <div>
                <button @click="clearCompleted">Clear completed</button>
            </div>

        </div>

    </div>
</template>

<script>
import todoItem from './todoItem.vue'

export default {
 name: 'todolist',
 components:{
    todoItem
 },
 data(){
      return {
          newTodo: '',
          id: 1,
          description: '',
          todos: [],
          filter: 'all',
          text: '' //for computed method search 
      }
 },
 methods: {

     addTodo(){ //create a new todo
         if(this.newTodo.length === 0){ //need to write a name at least one letter to create a todo 
             return
         }
         if(this.description.length === 0){ //need to write a description at least one letter to create a todo
             return
         }
         
         this.todos.push({
             id: this.id,
             title: this.newTodo,
             description: this.description,
             date: new Date().toDateString(),
             status: false,
             priority: 0
         })

         this.newTodo = ''
         this.description = ''
         this.id++
         this.updateLocal()
    },
    updateLocal(){ // method to update local storage
            localStorage.setItem('todos', JSON.stringify(this.todos))
    },
    changeStatus(index){ //change priority of a todo
        this.todos[index].status = !this.todos[index].status
        this.updateLocal()
    },
    changePriority(todoItem){ // chanfe priority of a todo
        this.todos[todoItem.index].priority = todoItem.prio
        this.updateLocal()
    },
    removeTodo(id){ //remove a todo
        const index = this.todos.findIndex((item) => item.id == id)
        this.todos.splice(index, 1)
        this.updateLocal()
    },
    clearCompleted(){ //remove all todos completed
        this.todos = this.todos.filter(todo => !todo.status)
        this.updateLocal()
    }
    },
    computed:{
        remaining() {
            return this.todos.filter(todo => !todo.status).length
        },
        todosFiltered() { //computed method to filter by all,active and completed. Besides sort by priority level.
            let filteredStatus = [] //all, active and completed
            if (this.filter == 'all') {
                filteredStatus = this.todos
            } else if (this.filter == 'active') {
                filteredStatus = this.todos.filter(todo => !todo.status)
            } else if (this.filter == 'completed') {
                filteredStatus = this.todos.filter(todo => todo.status)
            }else{
                filteredStatus = this.todos
            }

            return filteredStatus.sort((a,b) => a.priority - b.priority) //priority
        },
        search() { //computed method to filter by title of a todo. doesnt work yet
            return this.books.filter(book => {
                return book.titulo.toLowerCase().includes(this.text.toLowerCase());
            })
        }
        
    },
    mounted(){  //get todos array into local storage
        if(JSON.parse(localStorage.getItem('todos')))
            this.todos = JSON.parse(localStorage.getItem('todos'));
    }
 }

</script>

<style>
@import url("https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.5.2/animate.min.css");

/* general styles of my todo list*/
.todo-input {
    width: 100%;
    padding: 10px 18px;
    font-size: 18px;
    margin-bottom: 16px;
}
.todo-btn{
    border: none;
	font-family: inherit;
	font-size: inherit;
	color: inherit;
	background: none;
	cursor: pointer;
	padding: 5px 15px;
	display: inline-block;
	margin-bottom: 10px;
	text-transform: uppercase;
	letter-spacing: 1px;
	font-weight: 700;
	outline: none;
	position: relative;
	-webkit-transition: all 0.3s;
	-moz-transition: all 0.3s;
	transition: all 0.3s;

    border: 3px solid rgb(44, 62, 81);
	color: rgb(0, 0, 0);


}
.todo-btn:hover,
.todo-btn:active {
    color: rgb(255, 255, 255);
	background: rgb(52, 128, 228);
}

.todo-item {
    margin-bottom: 12px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    animation-duration: 0.3s;
}

.todo-item-left {
    display: flex;
    align-items: center;
}

.todo-item-label {
    padding: 10px;
    border: 1px solid white;
    margin-left: 12px;
}

.remove-item{
    cursor: pointer;
    margin-left: 14px;
}
.remove-item:hover {
    color: black;
    
}

.status {
    text-decoration: line-through;
    color: grey;
}

.extra-container {
    display: flex;
    align-items: center;
    justify-content: space-between;
    font-size: 16px;
    border-top: 1px solid lightgrey;
    padding-top: 14px;
    margin-bottom: 14px;
}
button {
    font-size: 14px;
    background-color: white;
    appearance: none;
}
button:hover {
    background: rgb(72, 217, 243);
}
button:focus {
    outline: none;
}
.active {
    background: rgb(52, 128, 228);
}
</style>
