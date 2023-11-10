<template>
	<ul class="todo-list">
		<app-todo-item v-for="todo in todos" :key="todo.id" :todo="todo"></app-todo-item>
	</ul>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import AppTodoItem from './AppTodoItem.vue';

interface State {
	todos: {
		id: number;
		text: string;
		complited: boolean;
	}[];
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
});
</script>
