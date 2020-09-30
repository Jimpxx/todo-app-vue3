<template>
  <div class="container">
    <h1 class="center-align">Todo App</h1>
    <form @submit.prevent="addTodo">
      <div class="input-field col">
        <input type="text" id="todo" v-model="text" />
        <label for="todo">Todo</label>
      </div>
    </form>
    <ul v-if="todos.length" class="collection">
      <li
        :class="{ done: todo.done }"
        class="collection-item"
        v-for="(todo, index) in todos"
        :key="todo.id"
      >
        <div class="todo-wrapper">
          <div class="left">
            <a href="#!" @click="toggleDone(index)"
              ><i class="material-icons">check</i></a
            ><span @click="toggleDone(index)" class="content">{{
              todo.content
            }}</span>
          </div>
          <div class="right">
            <a href="#!" class="secondary-content" @click="deleteTodo(index)"
              ><i class="material-icons">delete</i></a
            >
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
  import { reactive, ref } from 'vue';

export default {
  name: 'App',
  components: {},
  setup() {
    const todos = ref([]);
    const text = ref('')
    
    function addTodo() {
      const currentTodo = reactive({
      id: Date.now(),
      done: false,
      content: text.value,
      })
      todos.value.push(currentTodo)
      text.value = ''
    }
    function toggleDone(index) {
      todos.value[index].done = !todos.value[index].done;
    }
    function deleteTodo(index) {
      todos.value.splice(index, 1);
    }
    return {
      deleteTodo,
      toggleDone,
      text,
      todos,
      addTodo,
    }
  },
}
</script>

<style lang="scss">
.done {
  text-decoration: line-through;
}

.todo-wrapper {
  display: flex;
  justify-content: space-between;
}

.left {
  display: flex;
  align-items: center;
}

.content {
  margin-left: 1rem;
}
</style>
