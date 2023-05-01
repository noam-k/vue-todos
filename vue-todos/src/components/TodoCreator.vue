<template>
    <div class="input-wrap" :class="{ 'input-err' : todoState.invalid}">
        <input type="text" v-model="todoState.todo"/>
        <TodoButton @click="createTodo()"> Create </TodoButton>
    </div>
    <p v-show="todoState.invalid" class="err-msg">{{ todoState.errorMessage }}</p>
</template>

<script setup>
import { reactive } from 'vue';
import TodoButton from "./TodoButton.vue"

const emit = defineEmits(["create-todo"]);

const todoState = reactive({
    todo: "",
    invalid: false,
    errorMessage: "",
});

const createTodo = () => {
    todoState.invalid = false;
    if (todoState.todo !== "") {
        console.log(todoState.todo)
        emit("create-todo", todoState.todo);
        todoState.todo = "";
        return;
    }
    todoState.invalid = true;
    todoState.errorMessage = "Value cannot be empty"
}

</script>

<style lang="scss" scoped>
.input-wrap {
  display: flex;
  transition: 250ms ease;
  border: 2px solid #41b080;
  &.input-err {
    border-color: red;
  }
  &:focus-within {
    box-shadow: 0 -4px 6px -1px rgb(0 0 0 / 0.1),
      0 -2px 4px -2px rgb(0 0 0 / 0.1);
  }
  input {
    width: 100%;
    padding: 8px 6px;
    border: none;
    &:focus {
      outline: none;
    }
  }
}
.err-msg {
  margin-top: 6px;
  font-size: 12px;
  text-align: center;
  color: red;
}
</style>