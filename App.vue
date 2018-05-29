<template>
  <view class="container">
    <!-- <image source={{uri: 'https://images.template.net/wp-content/uploads/2014/06/42567177.jpg'}} style='image-style'/> -->
    <view class="text-input-container">
      <view class="text-input-wrapper">
        <text-input placeholder = 'Enter new todo'  v-bind:on-change-text = 'handleOnChangeText' v-model="newTodo"/>
      </view>
      <touchable-opacity class="add-button" title="Button" v-bind:on-press='handleAddPress' v-bind:disabled='emptyInput'>
        <text class="text-color-primary">ADD</text>
      </touchable-opacity>
    </view>
    <scroll-view>
      <view class='todo-wrapper' v-for='(todo, index) in todos' :key='index'>
        <touchable-opacity v-bind:on-press="() => onTaskPressed(index)">
          <text v-bind:class="{'text-task-completed': todo.isCompleted, 'text-todo-task': !todo.isCompleted}">
            • {{todo.task}}
          </text>
        </touchable-opacity>
        <touchable-opacity v-bind:on-press="() => handleDeletePress(index)">
          <text class="text-color-primary">
            x
          </text>
        </touchable-opacity>
      </view>
    </scroll-view>
  </view>
</template>

<script>
export default {
  data: function() {
    return {
      newTodo: undefined,
      todos: [],
      emptyInput: true,
      taskStyle: 'text-todo-task'
    };
  },
  methods: {
    handleAddPress: function() {
      let todo = {
        task: this.newTodo,
        isCompleted: false
      }
      this.todos.push(todo)
      this.newTodo = ''
      this.emptyInput = true
    },
    onTaskPressed: function(index) {
      this.todos[index].isCompleted = !this.todos[index].isCompleted
      console.log(this.todos, 'Check 123')
    },
    handleDeletePress: function(index) {
      this.todos.splice(index, 1)
    },
    handleOnChangeText: function(text) {
      this.newTodo = text
      if (text === '') this.emptyInput = true
      else this.emptyInput = false
    }
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
.text-color-primary {
  color: rgba(0, 0, 0, 0.767);
}
.text-todo-task {
  color:grey;
}
.text-task-completed {
  color: rgba(201, 29, 29, 0.534);
  text-decoration-line: line-through;
}
.button-primary {
  background-color: white;
  padding: 5
}
.text-input-wrapper {
  flex: 1;
  border-width: 1;
  border-color: rgb(112, 84, 46);
  justify-content: center;
  padding: 10
}
.text-input-primary {
  flex: 1;
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
.add-button {
  background-color: rgba(201, 29, 29, 0.534);
  padding-horizontal: 10;
  justify-content: center;
}
.text-input-container {
  margin-horizontal: 15;
  flex-direction: row;
  padding-bottom: 20
}
</style>
