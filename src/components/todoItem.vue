<template>
    <!-- Todo Item-->
    <div class="todo-item">
        <div class="todo-item-left">
                <!-- checkbox-->
                <input type="checkbox" @click="changedStatus(index,status)" >
                <!-- Todo info-->
                <div class="todo-item-label" >
                   <div>{{title}}</div>
                   <div>{{description}}</div>
                   <div>{{date}}</div>
                </div>
        </div>

        <!-- buttons to change priority of a todoItem-->
        <div>
            <button @click="changedPriority(index, 0)">High</button>
            <button @click="changedPriority(index, 1)">Medium</button>
            <button @click="changedPriority(index, 2)">Low</button>
        </div>
        <!-- div to remove a todo -->
        <div class="remove-item" @click="removedTodo(todo.id)">
            🗑️
        </div>
    </div>
</template>

<script>


export default ({
    name: 'todoItem',
    props: {
        todo:{
            type: Object,
            required: true
        },
        index: {
            type: Number,
            required: true
        }
    },
    data() {
        return {
            'id':this.todo.id,
            'title':this.todo.title,
            'description':this.todo.description,
            'date':this.todo.date,
            'status':this.todo.status,
            'priority':this.todo.priority
        }
    },
    methods: {
        removedTodo(id) { //event to remove a todo
            this.$emit('removedTodo', id)
        },
        changedStatus(index){ //event to change status of a todo
            this.$emit('changedStatus', index)
        },
        changedPriority(i, p){ //event to change priority of a todo
            this.$emit('changedPriority',{
                'index': i,
                'prio': p
            })
        }
    }
    
})
</script>