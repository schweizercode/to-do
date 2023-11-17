<template>
  <div class="best-todo">
    <div class="title has-text-centered">My Top To Do's</div>

    <form @submit.prevent="addTodo">
      <div class="field is-grouped mb-5">
        <p class="control is-expanded">
          <input 
          v-model="newTodoContent"
          class="input" 
          type="text" 
          placeholder="Add a TO DO" />
        </p>
        <p class="control">
          <button 
          :disabled="!newTodoContent"
          class="button is-success">Add</button>
        </p>
        </div>
    </form>

    <div 
    v-for="todo in todos" 
    class="card mb-5" 
    :key="todo.id"
    :class="{ 'has-background-success-light' : todo.done 
  }"
    >
      <div class="card-content">
        <div class="content">

       <div
         class="columns is-mobile is-vcentered">

         <div
         class="column"
         :class="{ 'has-text-success line-through' : todo.done }"
         >
         {{ todo.content }}
         </div>

            <div class="column is-5 has-text-right">
              <button 
              @click="toggleDone(todo.od)"
              class="button"
              :class="todo.done ? 'is-success' : 'is-light'"
              >
              &check;
            </button>

          <button
            @click="deleteTodo(todo.id)"
            class="button is-danger ml-2 mt-2">&cross;</button>             
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { v4 as uuidv4 } from 'uuid';

const todos = ref([
  {
    id: "id1",
    content: "Get dressed!",
    done: false,
  },

  {
    id: "id2",
    content: "Do my Dishes",
    done: true,
  },
]);

const newTodoContent = ref("")

const addTodo = () => {
 const newTodo = {
  id: uuidv4(),
  content: newTodoContent.value,
  done: false
 }
 todos.value.unshift(newTodo)
 newTodoContent.value = ""
};

const deleteTodo = id => {
  todos.value = todos.value.filter(todo => todo.id !== id)
}

const toggleDone = id => {
  console.log('toggleDone', id)
}
</script>

<style>
@import "bulma/css/bulma.min.css";

.best-todo {
  max-width: 400px;
  padding: 20px;
  margin: 0 auto;
}

.line-through {
  text-decoration: line-through;
}
</style>
