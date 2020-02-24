<template>
  <div class="todo-item__wrapper">
    <TodoItem
      v-for="todo in todos"
      :todo="todo"
      :key="`key-$${todo.id}`"
      @handleCheckTodo="$emit('handleCheckTodo', todo.id)"
      @handleRemoveTodo="$emit('handleRemoveTodo', todo.id)"
    />
  </div>
</template>

<script>
import TodoItem from "@/components/TodoItem";
export default {
  props: {
    todos: {
      type: Array,
      required: true
    }
  },
  components: {
    TodoItem
  }
};
</script>

<style lang="scss">
.todo {
  &-item__wrapper {
    display: inline-block;
    width: 600px;
  }
}
</style>
