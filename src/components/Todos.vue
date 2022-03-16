<template>
  <div class="todos">
    <!-- Add the appropriate event to the input. 
         Make sure it calls the function "addTodo" when you press enter. -->
    <input type="text" v-model="newTodo" placeholder="Add a new todo..." />
    <div v-if="todos.length">
      <ul>
        <!-- Add a click event to the li below, so that it calls the method deleteTodo, 
             make sure to include the id of todo in the parameters.-->
        <li v-for="todo in todos" :key="todo.id">
          {{ todo.text }}
        </li>
      </ul>
    </div>
    <!-- Add a class to the Div below, 
         so that it is only shown if the above condition of the Div above is false.-->
    <div>Woohoo, nothing left todo!</div>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  setup(props, { emit }) {
    const todos = ref([
      { text: "make the bed", id: 1 },
      { text: "play video games", id: 2 },
    ]);
    const newTodo = ref("");

    const addTodo = () => {
      if (newTodo.value) {
        // Change the id value below
        // Make sure that it receives a random number each time.
        const id = 4;
        todos.value = [{ text: newTodo.value, id }, ...todos.value];
        newTodo.value = "";
      } else {
        emit("badValue");
      }
    };

    // Fix this method after addTodo.
    const deleteTodo = (id) => {
      // Make sure that filters according to the right value.
      todos.value = todos.value.filter((todo) => todo.id == id);
    };

    return { todos, addTodo, deleteTodo, newTodo };
  },
};
</script>

<style>
.todos {
  max-width: 400px;
  margin: 20px auto;
  position: relative;
}
input {
  width: 100%;
  padding: 12px;
  border: 1px solid #eee;
  border-radius: 10px;
  box-sizing: border-box;
  margin-bottom: 20px;
}
.todos ul {
  position: relative;
  padding: 0;
}
.todos li {
  list-style-type: none;
  display: block;
  margin-bottom: 10px;
  padding: 10px;
  background: white;
  box-shadow: 1px 3px 5px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
  width: 100%;
  box-sizing: border-box;
}
.todos li:hover {
  cursor: pointer;
}
</style>