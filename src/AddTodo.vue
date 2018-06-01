<template>
  <view class="text-input-container">
    <view class="text-input-wrapper">
      <text-input placeholder = 'Enter new todo' v-model="newTodo"/>
    </view>
    <touchable-opacity class="add-button" title="Button" :on-press='addTodo' :disabled="(newTodo === '')">
      <text class="text-color-primary">ADD</text>
    </touchable-opacity>
  </view>
</template>

<script>
export default {
  data: function() {
    return {
      newTodo: ''
    };
  },
  props: {
    onAdd: Function
  },
  methods: {
    addTodo: function() {
      let todo = {
        task: this.newTodo,
        isCompleted: false,
        edited: false
      }
      this.onAdd(todo)
      this.newTodo = ''
    },
  }
}
</script>
>
 
<style>
.text-color-primary {
  color: rgba(0, 0, 0, 0.767);
}
.text-input-wrapper {
  flex: 1;
  border-width: 1;
  border-color: rgb(112, 84, 46);
  justify-content: center;
  padding: 10
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
