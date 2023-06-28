<script setup>
import { computed, reactive, ref } from 'vue';
import Todo from './components/Todo.vue';
const todos = reactive([]);
const activeTodos = computed(()=>todos.filter((todo)=>!todo.isDone).length);
const todoInput = ref("");
function addNewTodo() {
  const newTodo = {
    id:Date.now(),
    createdAt:new Date().toISOString(),
    title:todoInput.value,
    isDone:false
  };
  todos.unshift(newTodo);
  todoInput.value = "";
}
function deleteTodo(index) {
  todos.splice(index,1);
}
function handleComplete(index) {
  todos[index].isDone=!todos[index].isDone;
}
</script>

<template>
<header class="header">
  <h1>Todo list</h1>
</header>
  <section class="container">
    <div class="form-container">
      <form @submit.prevent="addNewTodo">
        <input type="text" name="" class="todo-input" placeholder="Add new todo..." autofocus v-model="todoInput"/>
          <button type="submit" class="todo-button" :disabled="!todoInput">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" width="28" stroke-width="1.5" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" d="M12 9v6m3-3H9m12 0a9 9 0 11-18 0 9 9 0 0118 0z" />
            </svg>
          </button>
      </form>
   </div>
   <template v-if="todos.length">
      <div class="todo-container">
        <todo v-for="(todo,index) in todos" :todo="todo" :key="todo.id" @delete="deleteTodo(index)" @complete="handleComplete(index)"/>
      </div>
      <footer>
        <p v-if="activeTodos">{{ activeTodos }} Active Todos</p>
        <p v-else>Nothing todo, have some rest...</p>
      </footer>
    </template>
   <div v-else class="todo-container add-first-todo">
      <div class="todo">
        <p class="">Add Your First Todo</p>
      </div>
   </div>
  </section>
</template>

<style scoped>
.header{
    min-height: 20vh;
    display: flex;
    align-items: center;
    justify-content: center;
}

.container{
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
}

.form-container{
    display: flex;
}

.todo-container{
    width: 25rem;
    display: flex;
    flex-direction: column;
    margin-top: .3rem;
}

.add-first-todo{
  opacity: .5;
}

.todo-button{
  display: flex;
  justify-content: center;
  align-items: center;
}

form{
    width: 25rem;
    background-color: #fff;
    display: flex;
    justify-content: space-between;
    overflow: hidden;
    border-radius: 8px;
    border: 2px solid var(--secondaryColor);
}

form input{
    flex:1;
}

form input,form button{
    border: none;
    outline: none;
    background-color: var(--mainWhite);
    font-size: 1rem;
    padding: .5rem;
}

form button{
    color: var(--primaryColor);
    cursor: pointer;
    transition: all .2s ease-in-out;
    background-color: var(--secondaryColor);
}

form button:hover{
    background-color: var(--primaryColor);
    color: var(--mainWhite);
}

input{
    font-family: inherit;
}

select {
    font-family: inherit;
    border: none;
    outline: none;
    appearance: none;
    padding: 1rem;
    color: var(--primaryColor);
    width: 100%;
    border-radius: 8px;
    border: 2px solid var(--secondaryColor);
}

.select{
    margin-left: 1rem;
    cursor: pointer;
    width: 10rem;
    font-weight: bold;
    position: relative;
}

.select::after{
    content: "\25BC";
    position: absolute;
    right: 0;
    top: 0;
    padding: 1rem;
    color: var(--primaryColor);
    pointer-events: none;
    transition: all .3s ease-in-out;
}

.todo{
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: var(--secondaryColor);
    margin: .3rem 0;
    transition: all .2s ease;
}

.todo p{
    flex: 1;
    color: var(--primaryColor);
    font-weight: bold;
    padding: .8rem .5rem;
    background-color: var(--bodyColor);
    text-align: center;
}

footer{
  margin-top: .5rem;
  width: 25rem;
  text-align: center;
  color: var(--primaryColor);
}
</style>
