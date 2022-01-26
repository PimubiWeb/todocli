<template>
    <div class="todo-item">
        <div class="todo-item-left">
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
    </div>
</template>

<script>


export default ({
    name: 'todoItem',
    props: [todo,index]
}),
</script>
