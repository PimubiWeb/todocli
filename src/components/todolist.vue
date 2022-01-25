<template>
  <div class="container">
       <input type="text" class="todo-input" placeholder="Enter a title todo"
       v-model="newTodo" @keyup.enter="addTodo">
        <input type="text" class="todo-input" placeholder="Enter a description todo"
       v-model="description" @keyup.enter="addTodo">
       <button @click="addTodo" class="todo-btn">Add</button>
       <div v-for="todo in todos" :key="todo.id" class="todo-item">
           <div>
               {{todo.title}} - {{todo.description}} - {{todo.fecha}} - {{todo.priority}}
           </div>
           <div class="remove item">
               🗑️
           </div>
           
       </div>
       
  </div>
</template>

<script>
export default {
 name: 'todolist',

 data(){
      return {
          newTodo: '',
          id: 3,
          description: '',

          todos: [
              {
                  'id':1,
                  'title': 'Vue',
                  'description': 'is a todo\'s project',
                  'fecha': new Date().toDateString(),
                  'status': false,
                  'priority': 0 //0 high, 1 medium, 2 low
              },
              {
                  'id':2,
                  'title': 'JS',
                  'description': 'is a shit\'s project',
                  'fecha': new Date().toDateString(),
                  'status': false,
                  'priority': 0 //0 high, 1 medium, 2 low
              }
          ]
      }
 },
 methods: {
     addTodo(){
         this.todos.push({
             id: this.id,
             title: this.newTodo,
             description: this.description,
             fecha: new Date().toDateString(),
             status: false,
             priority: 0
         })

         this.newTodo = ''
         this.description = ''
         this.id++
     }
 }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
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

    border: 3px solid rgb(0, 0, 0);
	color: rgb(0, 0, 0);


}
.todo-btn:hover,
.todo-btn:active {
    color: rgb(32, 179, 101);
	background: rgb(0, 0, 0);
}

.remove-item {
    cursor: crosshair;
    margin-left: 14px;
}
.remove-item:hover {
    color: black;
    
}


</style>
