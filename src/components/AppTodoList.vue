<template>
	<ul class="todo-list">
		<app-todo-item
			v-for="todo in todos"
			:key="todo.id"
			:todo="todo"
			@toggle-todo="toggleTodo"
			@remove-todo="removeTodo"
		></app-todo-item>
	</ul>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import AppTodoItem from './AppTodoItem.vue';
import { Todo } from '@/types/Todo';

interface State {
	todos: Todo[];
}

export default defineComponent({
	components: {
		AppTodoItem,
	},
	data(): State {
		return {
			todos: [
				{ id: 0, text: 'Выучить основы Vue', complited: true },
				{ id: 1, text: 'Выучить основы TypeScript', complited: false },
				{ id: 2, text: 'Ввыучить продвинутый уровень Vue', complited: false },
			],
		};
	},
	methods: {
		toggleTodo(id: number) {
			// console.log(id);
			const targetTodo = this.todos.find((todo: Todo) => todo.id === id);

			if (targetTodo) {
				targetTodo.complited = !targetTodo.complited;
			}
		},
		removeTodo(id: number) {
			this.todos = this.todos.filter((todo: Todo) => todo.id !== id);
		},
	},
});
</script>
