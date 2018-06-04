<template>
  <view class='todo-wrapper'>
    <touchable-opacity :on-press='handleTaskPressed' v-if="!todo.edited">
      <text v-bind:class="[todo.isCompleted ? 'text-task-completed' : 'text-todo-task']">
        • {{todo.task}}
      </text>
    </touchable-opacity>
    <view class="task-input-wrapper" v-if="todo.edited">
      <text-input placeholder='Enter Task' v-model='editedTask'/>
    </view>
    <view class='todo-button-wrapper' v-if="todo.edited">
      <touchable-opacity :on-press="checkIconPress" class='done-button'>
        <image :source='checkIcon' class='image-style'/>
      </touchable-opacity>
      <touchable-opacity v-bind:on-press="cancelIconPress" class='done-button'>
        <image :source='crossIcon' class='image-style'/>
      </touchable-opacity>
    </view>
    <view class='todo-button-wrapper' v-if="!todo.edited">
      <touchable-opacity :on-press="editIconPress" class='edit-button'>
        <image :source='editIcon' class='image-style'/>
      </touchable-opacity>
      <touchable-opacity :on-press="deleteIconPress">
        <image :source='crossIcon' class='image-style'/>
      </touchable-opacity>
    </view>
  </view>
</template>

<script>

import editIcon from '../assets/edit_icon.png';
import crossIcon from '../assets/cross_icon.png';
import checkIcon from '../assets/check_icon.png';

export default {
  data: function() {
    return {
      editedTask: this.todo.task,
      editIcon,
      crossIcon,
      checkIcon
    };
  },
  props: {
    todo: Object,
    selectedIndex: Number,
    editTodo: Function,
    deleteTodo: Function,
    cancelEdit: Function,
    toggleTaskStatus: Function,
    editPressed: Function
  },
  methods: {
    editIconPress: function() {
      this.editPressed(this.selectedIndex)
    },
    checkIconPress: function() {
      if (this.editedTask !== '')
        this.editTodo(this.selectedIndex, this.editedTask)
      else {
        this.editedTask = this.todo.task
        this.cancelEdit(this.selectedIndex)
      }
    },
    cancelIconPress: function() {
      this.cancelEdit(this.selectedIndex)
    },
    handleTaskPressed: function() {
      this.toggleTaskStatus(this.selectedIndex)
    },
    deleteIconPress: function(index) {
      this.deleteTodo(this.selectedIndex)
    },
  }
}
</script>
>
 
<style>
.todo-button-wrapper {
  flex-direction: row
}
.done-button {
  margin-left: 20
}
.image-style {
  height: 20;
  width: 20;
}
.edit-button {
  padding-right: 20
}
.text-todo-task {
  color:grey;
}
.text-task-completed {
  color: rgba(201, 29, 29, 0.534);
  text-decoration-line: line-through;
}
.task-input-wrapper {
  flex: 1;
  border-width: 1;
  border-color: rgba(201, 29, 29, 0.534);
  justify-content: center;
  padding: 10
}
.todo-wrapper {
  justify-content: space-between;
  align-items: center;
  flex-direction: row;
  flex: 1;
}
</style>
