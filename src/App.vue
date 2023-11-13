<template>
	<app-header></app-header>

	<app-filters :active-filter="activeFilter" @set-filter="setFilter"></app-filters>

	<main class="app-main">
		<app-todo-list
			:todos="filteredTodos"
			@toggle-todo="toggleTodo"
			@remove-todo="removeTodo"
		></app-todo-list>

		<app-add-todo @add-todo="addTodo"></app-add-todo>
	</main>

	<app-footer :stats="stats"></app-footer>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import AppHeader from './components/AppHeader.vue';
import AppFilters from './components/AppFilters.vue';
import AppTodoList from './components/AppTodoList.vue';
import AppAddTodo from './components/AppAddTodo.vue';
import AppFooter from './components/AppFooter.vue';
import { Todo } from '@/types/Todo';
import { Filter } from '@/types/Filter';

interface State {
	todos: Todo[];
	activeFilter: Filter;
}

interface Stats {
	active: number;
	done: number;
}

export default defineComponent({
	components: {
		AppHeader,
		AppFilters,
		AppTodoList,
		AppAddTodo,
		AppFooter,
	},
	data(): State {
		return {
			todos: [
				{ id: 0, text: 'Выучить основы Vue', completed: true },
				{ id: 1, text: 'Выучить основы TypeScript', completed: false },
				{ id: 2, text: 'Ввыучить продвинутый уровень Vue', completed: false },
			],
			activeFilter: 'All',
		};
	},
	computed: {
		filteredTodos(): Todo[] {
			switch (this.activeFilter) {
				case 'Active':
					return this.activeTodos;
				case 'Done':
					return this.doneTodos;
				case 'All':
				default:
					return this.todos;
			}
		},
		stats(): Stats {
			return {
				active: this.activeTodos.length,
				done: this.doneTodos.length,
			};
		},
		activeTodos(): Todo[] {
			return this.todos.filter((todo) => !todo.completed);
		},
		doneTodos(): Todo[] {
			return this.todos.filter((todo) => todo.completed);
		},
	},
	methods: {
		addTodo(todo: Todo) {
			this.todos.push(todo);
		},
		toggleTodo(id: number) {
			// console.log(id);
			const targetTodo = this.todos.find((todo: Todo) => todo.id === id);

			if (targetTodo) {
				targetTodo.completed = !targetTodo.completed;
			}
		},
		removeTodo(id: number) {
			this.todos = this.todos.filter((todo: Todo) => todo.id !== id);
		},
		setFilter(filter: Filter) {
			this.activeFilter = filter;
		},
	},
});
</script>
