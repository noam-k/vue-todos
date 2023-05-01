<script setup>
  import TodoCreator from "../components/TodoCreator.vue";
  import { uid } from "uid";
  import { ref } from "vue"; 
  import TodoItem from "../components/TodoItem.vue";
  import { Icon } from "@iconify/vue";

  const todoList = ref([]);

  const fetchTodoList = () => {
    const savedTodoList = JSON.parse(localStorage.getItem("todoList"));
    if (savedTodoList) {
      todoList.value = savedTodoList;
    }
  }

  fetchTodoList();

  const setTodoListLocalStorage = () => {
    localStorage.setItem("todoList", JSON.stringify(todoList.value));
  }

  const createTodo = (todo) => {
    console.log(todoList.length);
    todoList.value.push({
      id: uid(),
      todo,
      isCompleted: null,
      isEditing: null,
    });
    setTodoListLocalStorage();
  }

  const toggleTodoComplete = (index) => {
    todoList.value[index].isCompleted = !todoList.value[index].isCompleted;
    setTodoListLocalStorage();
  }

  const toggleEditTodo = (index) => {
    todoList.value[index].isEditing = !todoList.value[index].isEditing;
    setTodoListLocalStorage();
  }

  const updateTodo = (updatedValue, index) => {
    todoList.value[index].todo = updatedValue;
    setTodoListLocalStorage();
  }

  const deleteTodo = (todoId) => {
    todoList.value = todoList.value.filter((todo) => todo.id !== todoId);
    setTodoListLocalStorage();
  }
</script>

<template>
  <main>
    <h1>Create Todo</h1>
    <TodoCreator @create-todo="createTodo"/>
    <ul v-if="todoList.length > 0" class="todo-list">
      <TodoItem
        v-for="(todo, index) in todoList"
        :todo="todo"
        :index="index"
        @toggle-complete="toggleTodoComplete"
        @edit-todo="toggleEditTodo"
        @update-todo="updateTodo"
        @delete-todo="deleteTodo"
      />
    </ul>
    <p v-else class="todos-msg">
      <Icon icon="noto:relieved-face" width="22"/>
      <span>Congratulations, no tasks to complete</span>
    </p>
  </main>
</template>

<style scoped lang="scss">
main {
  display: flex;
  flex-direction: column;
  max-width: 500px;
  width: 100%;
  margin: 0 auto;
  padding: 40px 16px;
  h1 {
    margin-bottom: 16px;
    text-align: center;
  }
  .todo-list {
    display: flex;
    flex-direction: column;
    list-style: none;
    margin-top: 24px;
    gap: 20px;
  }
  .todos-msg {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    margin-top: 24px;
  }
}
</style>