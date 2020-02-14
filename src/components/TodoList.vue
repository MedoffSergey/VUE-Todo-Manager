// Описание задачи
// 1. Починить код
// 2. Добавить кнопку и функцию удаления задачи
// 3. Посмотреть на код и
// 3.1. Перечислить, что бы вы сделали по-другому
// 3.2. [опционально] Переписать код как душа просит
// Комментарии по ошибкам можно писать прямо в коде

// 1 Починил код
// 2 Добавил кнопку удаления задачи
// 3 Установил checkbox для замены статуса задач




<template>
	<div id="TodoList">
		<input type="text" class="todo-input" autofocus placeholder="Новая задача" v-model="newTodo" @keyup.enter="addTodo">
		<button class="add-todo-btn" v-on:click="addTodo">
			<img src="https://image.flaticon.com/icons/svg/748/748113.svg" width="25px" alt="">
		</button>
		<div class="errorMsg" v-if="errorMsg">
			<span>Поле пустое</span>
		</div>
		<!-- -->
		<div class="extra-container">
			<div>
				<button :class="{ active: filter === 'all' }" @click="filter = 'all'">Все</button>
				<button :class="{ active: filter === 'active' }" @click="filter = 'active'">Активные</button>
				<button :class="{ active: filter === 'completed' }" @click="filter = 'completed'">Завершенные</button>
			</div>
		</div>
		<TodoItem :items="todosFiltered"></TodoItem>

	</div>
</template>

<script>
	import TodoItem from './TodoItem.vue'

	export default {
		name: 'TodoList',
		components: {
			TodoItem
		},

		data() {
			return {
				// zadachi: [], //перевел бы на английский
				newTodo: '',			//	переменная для задачи
				filter: 'all',		//	переменная для фильра
				errorMsg: false,	//	переменная вывода ошибки

				todos: [					// задачи по умолчанию для примера
					{
						'title': 'Купить хлеб',		//наименование задачи
						'completed': false				//статус задачи
					},
					{
						'title': 'Купить Молоко',
						'completed': true
					}
				]
			}
		},

		// DOM ещё не построен, .document.getElementById("search")  не сработает
		// установил на input
		// Атрибут autofocus устанавливает, что кнопка получает фокус после загрузки страницы.
		//  Такую кнопку можно нажать сразу без перевода на неё фокуса, например, с помощью клавиатуры.
		// created() {
		//   var search = document.getElementById("search") || {};
		//   search.focus();
		// },

		computed: {
			todosFiltered() {																				//	Фильтр
				if (this.filter ==='all')															//	Если установлен на все то,
					return this.todos;																	//	возвращаем Весь список задач.
				else if (this.filter === 'active')										//	Если установлен на активные,
					return this.todos.filter(todo => !todo.completed);	//	возвращаем отфильтрованный с активными задачами.
				else if (this.filter === 'completed')									//	Если установлен на Завершенные,
					return this.todos.filter(todo => todo.completed);		//	возвращаем отфильтрованный с завершенные задачами.

				return this.todos																			// Возвращаем весь список если категория фильтра не установлена
			}
		},

		methods: {
			addTodo() {
				if (this.newTodo.trim().length !== 0) {		//	Проверяем что input не пустой и отсутвуют пробелы в поле
					this.errorMsg = false;									//	Если не пустое то не выводим сообщение об ошибке
				}	else {																	//	Иначе
					this.errorMsg = true;										//	Выведем сообщение об ошибке
					return 0;																//	Прервываем функцию
				}


				this.todos.unshift({		//	Добавим элемент в начало массива
					title: this.newTodo,	//	Берем значение с input
					completed: false			//	По умолчанию устанавливаем статус выполнения в активный
				});
				this.newTodo = ''				//	Очистим поле
			}
		}
	}
</script>

<style scoped lang="scss">
	.todo-input {
		width: 510px;
		padding: 10px 15px;
		font-size: 16px;
		margin-bottom: 10px;


		&:focus {
			outline: none;
		}
	}

	.add-todo-btn {
		width: 50px;
		height: 45px;
		position: absolute;
		font-size: 34px;
		color: grey;
		margin-left: -1px;
	}

	.extra-container {
		display: flex;
		align-items: center;
		justify-content: space-between;
		font-size: 14px;
		border-bottom: 1px solid lightgray;
		padding-bottom: 14px;
		margin-bottom: 14px;
	}

	button {
		border: 1px solid grey;
		margin-left: 5px;
		padding: 2px;
		font-size: 16px;
		color: black;
		background-color: white;
		outline: none;
		border-radius: 4px;
		cursor: pointer;

		&:hover {
			cursor: pointer;
			background: #43B05C;
			color: white;
			transition: 0.3s;
		}

	}

	.active {
		border: 1px solid green;
		background: #43B05C;
		color: white;

	}

	.errorMsg{
		background-color: red;
		color: #fff;
		display: inline-flex;
		border-radius: 5px;
		padding: 5px 15px;
		margin-bottom: 5px;
		font-size: 14px;
	}

</style>
