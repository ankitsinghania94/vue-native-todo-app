<template>
  <view class="container">
    <AddTodo
      :onAdd='addTodo'
    />
    <scroll-view>
      <view class='todo-wrapper' v-for='(todo, index) in todos' :key='index'>
        <TodoItem
          :todo='todo'
          :selectedIndex='index'
          :onEditPressed='onEditPressed'
          :editTodo='editTodo'
          :deleteTodo='deleteTodo'
          :cancelEdit='cancelEdit'
          :onTaskPressed='onTaskPressed'
        />
      </view>
    </scroll-view>
  </view>
</template>

<script>
import AddTodo from './src/AddTodo'
import TodoItem from './src/TodoItem'

export default {
  data: function() {
    return {
      newTodo: '',
      todos: [],
      taskStyle: 'text-todo-task',
    };
  },
  components: {
    AddTodo,
    TodoItem
  },
  methods: {
    addTodo: function(todo) {
      this.todos.push(todo)
    },
    onEditPressed: function(index) {
      this.todos[index].edited = true
    },
    editTodo: function(index, editedTask) {
      this.todos[index].task = editedTask
      this.todos[index].edited = false
    },
    cancelEdit: function(index) {
      this.todos[index].edited = false
    },
    onTaskPressed: function(index) {
      this.todos[index].isCompleted = !this.todos[index].isCompleted
    },
    deleteTodo: function(index) {
      this.todos.splice(index, 1)
    },
  }
}
</script>
>
 
<style>
.container {
  background-color:white;
  flex: 1;
  padding-top: 40;
}
.todo-wrapper {
  margin-horizontal: 15;
  background-color: beige;
  justify-content: space-between;
  align-items: center;
  flex-direction: row;
  margin-vertical: 2.5;
  padding: 10;
  border-radius: 5;
}
</style>
