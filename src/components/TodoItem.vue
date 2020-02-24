<template>
  <div class="todo-item">
    <input 
		type="checkbox"
		@click="$emit('handleCheckTodo')"
		:checked="todo.complited"
		class="todo-item__checkbox"
	/>
    <p 
		@click="$emit('handleCheckTodo')"
		class="todo-item__title"
		:class="checked"
	>
			{{todo.title}}
	</p>
	<div @click="$emit('handleRemoveTodo')" class="todo-item__btn">
		<button class="todo-item__close">&times;</button>
	</div>
  </div>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true,
    }
  },
  computed: {
	checked() {
		return this.todo.complited ? 'todo-item__title--checked' : '';
	}
  }
};
</script>

<style lang="scss">
.todo-item {
	display: flex;
	justify-content: space-between;
	align-items: center;

	&:hover {
		.todo-item__close {
			display: inline;
		}
	}

	&__checkbox {
		margin: 0;
	}

	&__title {
		font-size: 18px;
		flex-basis: 100%;
		cursor: pointer;

		&--checked {
			text-decoration: line-through;
		}
	}

	&__btn {
		width: 30px;
	}

	&__close {
		vertical-align: middle;
		display: none;
		border: none;
		background: none;
		cursor: pointer;
		padding: 0;
		margin: 0;
		line-height: 30px;
		font-size: 20px;
		color: #bd2130;
	}
}
</style>

