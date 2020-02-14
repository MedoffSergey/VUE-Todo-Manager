<template>
<div id="TodoItem">
  <div v-for="(item, index) in items" :key="index" class="todo-item">
    <div class="todo-item-left">
      <input class="edit-item" type="checkbox" v-model="item.completed">

      <div v-if="!item.editing" @dblclick="editTodo(item)" class="todo-item-label" :class="{ completed : item.completed}">
        <span>{{item.title}}</span>
      </div>

    </div>
    <div class="remove-item" @click="removeItem(index)">
      <img src="https://image.flaticon.com/icons/svg/1828/1828843.svg" width="25px" alt="">
    </div>
  </div>
</div>
</template>

<script>
export default {
  props: ['items'],

  methods: {
    removeItem(index) {
      this.items.splice(index, 1)
    }
  }
}
</script>

<style scoped lang="scss">
.todo-item {
    max-width: 600px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    border: 1px solid #ccc;
    border-radius: 5px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.12);
    margin: 8px;
    padding: 16px;
}

.remove-item {
    cursor: pointer;
}

.edit-item {
    cursor: pointer;
}

.todo-item-left {
    display: flex;
    align-items: center;
}

.todo-item-label {
    padding: 10px;
    max-width: 600px;
    height: 20px;
    color: #000;
}

.completed {
    text-decoration: line-through;
    color: #898989;
}
</style>
