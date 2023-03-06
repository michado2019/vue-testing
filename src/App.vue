<template>
  <div class="todosWrapper">
    <TodosComponent />
    <div v-for="todo in todos" :key="todo.id" class="todosDiv">
      <h2 :class="{ todo: todo.isCompleted }">{{ todo.task }}</h2>
      <div class="todosBtn-div">
        <button @click="handleComplete(todo)">Complete</button>
        <button @click="handleDelete(todo.id)">Delete</button>
      </div>
    </div>
    <input type="text" placeholder="Add todo" v-model="todo" class="todoInput" />
    <button @click="addTodo" :disabled="!todo" class="addTodo-btn">Add todo</button>
  </div>
</template>
<script>

import TodosComponent from './components/TodosComponent.vue';
export default {
  name: "App",
  components: {TodosComponent},
  data() {
    return {
      todo: "",
      todos: [
        {
          id: 1,
          task: "Personal cleaning",
          isCompleted: false,
        },
      ],
    };
  },
  watch: {
    todos: {
      handler() {
        console.log("---->", this.todos);
        localStorage.setItem("todos", JSON.stringify(this.todos));
      },
      deep: true,
    },
  },
  methods: {
    addTodo() {
      this.todos.push({
        id: this.todos.length + 1,
        task: this.todo,
        isCompleted: false,
      });
    },
    handleComplete(todo) {
      todo.isCompleted = !todo.isCompleted;
    },
    handleDelete(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
  },
  mounted() {
    let todos = localStorage.getItem("todos");
    let parsedTodos = JSON.parse(todos);
    this.todos = parsedTodos;
  },
};
</script>
<style>
template{
  margin: 0;
  box-sizing: border-box;
  padding: 0;
}
.todosWrapper {
  display: flex;
  margin: 0 auto;
  width: 50%;
  border-radius: 10px;
  background-color: rgb(107, 17, 17);
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
.todosWrapper h1 {
  color: #042630;
}
.todosDiv {
  display: flex;
  align-items: center;
}
.todo {
  text-decoration: line-through;
  color: red;
}
.todoInput {
  border: 1px solid #eee;
  outline: none;
  width: 310px;
  padding: 10px 10px;
  border-radius: 4px;
  background-color: #eee;
}
.todosBtn-div {
  margin-left: 20px;
}
.todosBtn-div button {
  padding: 7px 20px;
  background-color: black;
  color: white;
  margin-left: 20px;
  border-radius: 5px;
  font-weight: 700;
  cursor: pointer;
}
.addTodo-btn {
  padding: 10px 20px;
  border-radius: 2px;
  border: 0;
  font-weight: 600;
  margin: 3px;
}
@media screen and (max-width: 890px) {
  .todosDiv {
    display: flex;
    flex-direction: column;
  }
  .todosBtn-div {
    margin-left: 0;
  }
  .todosBtn-div button {
  margin-left: 0;
}
  .addTodo-btn {
    margin: 3px 0;
  }
}
@media screen and (max-width: 700px) {
  .todosWrapper {
    width: 80%;
  }
}
</style>
