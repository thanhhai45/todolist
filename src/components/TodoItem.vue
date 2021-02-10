<template>
  <div>
    <p :class="['todo-item', item.completed && 'is-completed']">
      <input type="checkbox" :checked="item.completed" @change="markItemCompleted">
      {{item.title}}
      <button class="del-btn" @click="deleteItem">Delete</button>
    </p>
  </div>
</template> 

<script>
export default {
  name: 'TodoItem',
  props: ['item'],
  setup(props, context) {
    const markItemCompleted = () => {
      context.emit('item-completed', props.item.id)
    }

    const deleteItem = () => {
      context.emit('delete-item', props.item.id)
    }

    return {
      markItemCompleted, deleteItem
    }
  }
}
</script>

<style scoped>
.todo-item{
  background: #f4f4f4;
  padding: 10px;
  margin: 0;
  border-bottom: 1px #ccc dotted;
}
.del-btn {
  background: #ff0000;
  color: #fff;
  border: none;
  cursor: pointer;
  float: right;
  line-height: 20px;
  border-radius: 5px;
  font-size: 16px;
}
.is-completed {
  text-decoration: line-through;
}
</style>