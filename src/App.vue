<template>
  <div id="app" class="todo-list__wrapper">
    <div class="todo-list-header">
      <h1 class="todo-list-header__title">
        Todo application
      </h1>
      <input
        placeholder="Название задачи"
        class="todo-list-header__input"
        v-model="taskName"
        @keyup.enter="addNewTask"
        @change="findTaskName"
      />
    </div>
    <div class="todo-list-filter__wrapper">
      <a href="#" @click.prevent="fliterClosed" class="todo-list-filter__button">
        Закрытые
      </a>
      <a href="#" @click.prevent="fliterOpened" class="todo-list-filter__button">
        Открытые
      </a>
      <a href="#" @click.prevent="fliterAll" class="todo-list-filter__button">
        Все
      </a>
    </div>
    <TodoList
      v-bind:todos="filteredTodos"
      @handleCheckTodo="handleCheckTodo"
      @handleRemoveTodo="handleRemoveTodo"
    />
  </div>
</template>

<script>
import TodoList from "@/components/TodoList";
// import TodoInput from "@/components/TodoInput";

export default {
  name: 'app',
  data() {
    return {
      id: 1,
      todos: [],
      filter: '',
      taskName: '',
      filterTaskName: '',
    };
  },
  components: {
    TodoList,
  },
  methods: {
    addNewTask() {      
      this.todos.unshift(
        {id: ++this.id, title: this.taskName, complited: false}
      );
      this.taskName = '';
    },
    handleCheckTodo(id) {
      this.todos.forEach(todo => {
        if (todo.id === id) {
          todo.complited = !todo.complited;
        }
      })
    },
    handleRemoveTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
    },
    fliterClosed() {
      this.filter = 'closed';
    },
    fliterOpened() {
      this.filter = 'opened';
    },
    fliterAll() {
      this.filter = 'all';
    },
    findTaskName() {
      this.filterTaskName = this.taskName
    }
  },
  computed: {
    filteredTodos() {
      if(this.filter === 'closed') {
        return this.todos.filter(item => 
          item.complited && item.title.toLowerCase().includes(this.taskName.toLowerCase())
        );
      } else if (this.filter === 'opened') {
        return this.todos.filter(item =>
          !item.complited && item.title.toLowerCase().includes(this.taskName.toLowerCase())
        )
      } 
      return this.todos.filter(item =>
          item.title.toLowerCase().includes(this.taskName.toLowerCase())
      );
    }
  }
}

</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.todo-list {
  &__wrapper {
    width: 500px;
    margin: 0 auto;
  }

  &-header {
    width: 100%;
    padding: 20px;
    border-bottom: 1px solid rgba(0, 0, 0, 0.3);

    &__input {
      width: 400px;
      height: 20px;
      padding: 5px 15px;
      border: 0;
      border-bottom: 1px solid rgba(0, 0, 0, 1);
    }
  }
}

</style>
