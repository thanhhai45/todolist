<template>
  <div>
    <form @submit="addItem">
      <input type="text" placeholder="Việc mới..." v-model="title" />
      <input type="submit" value="Thêm" class="add-btn" />
    </form>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  name: 'AddTodo',
  setup(props, context) {
    const title = ref('')

    const addItem = event => {
      event.preventDefault()
      const newItem = {
        title: title.value,
        completed: false
      }

      context.emit('add-item', newItem)
      title.value = ''
    }

    return {
      title, addItem
    }
  }
}
</script>

<style scoped>
form{
  margin-top: 10px;
  display: flex;
}
input[type='text'] {
  flex: 10;
  padding: 5px;
}
input[type='submit'] {
  flex: 2;
  padding: 5px;
}

</style>