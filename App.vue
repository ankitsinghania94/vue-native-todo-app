<template>
  <view class="container">
    <!-- <img src="'https://images.template.net/wp-content/uploads/2014/06/42567177.jpg'"/> -->
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
        <touchable-opacity v-bind:on-press="() => onTaskPressed(index)" v-if="!todo.edited">
          <text v-bind:class="[todo.isCompleted ? 'text-task-completed' : 'text-todo-task']">
            • {{todo.task}}
          </text>
        </touchable-opacity>
        <view class="task-input-wrapper" v-if="todo.edited">
          <text-input placeholder='Enter Task' v-bind:on-change-text="(text) => handleOnChangeTask(text, index)" v-bind:value='todo.task'/>
        </view>
        <view class='todo-button-wrapper' v-if="todo.edited">
          <touchable-opacity v-bind:on-press="() => handleDonePress(index)" class='done-button'>
            <text class="text-color-primary">
              DONE
            </text>
          </touchable-opacity>
          <touchable-opacity v-bind:on-press="() => handleCancelPress(index)" class='done-button'>
            <text class="text-color-primary">
              X
            </text>
          </touchable-opacity>
        </view>
        <view class='todo-button-wrapper' v-if="!todo.edited">
          <touchable-opacity v-bind:on-press="() => handleEditPress(index)" class='edit-button'>
            <text class="text-color-primary">
              E
            </text>
          </touchable-opacity>
          <touchable-opacity v-bind:on-press="() => handleDeletePress(index)">
            <text class="text-color-primary">
              X
            </text>
          </touchable-opacity>
        </view>
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
      taskStyle: 'text-todo-task',
      editedText: ''
      // image: 'https://images.template.net/wp-content/uploads/2014/06/42567177.jpg'
    };
  },
  methods: {
    handleAddPress: function() {
      let todo = {
        task: this.newTodo,
        isCompleted: false,
        edited: false
      }
      this.todos.push(todo)
      this.newTodo = ''
      this.emptyInput = true
    },
    handleEditPress: function(index) {
      this.todos[index].edited = true
    },
    handleDonePress: function(index) {
      if (this.editedText !== '')
        this.todos[index].task = this.editedText
      this.todos[index].edited = false
    },
    handleCancelPress: function(index) {
      this.todos[index].edited = false
    },
    handleOnChangeTask: function(text, index) {
      this.editedText = text
    },
    onTaskPressed: function(index) {
      this.todos[index].isCompleted = !this.todos[index].isCompleted
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
.todo-button-wrapper {
  flex-direction: row
}
.done-button {
  margin-left: 40
}
.edit-button {
  padding-right: 20
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
.task-input-wrapper {
  flex: 1;
  border-width: 1;
  border-color: rgba(201, 29, 29, 0.534);
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
