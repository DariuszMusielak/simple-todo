<template>
  <div class="wrapper">
    <Claim v-model="loading"/>
    <NewTodoInput
      v-model="newTodo"
      v-on:create-todo="addTodo"
    />
    <div class="todosWrapper" v-if="todos && !loading">
      <TodoItem
        v-on:delete-todo="deleteTodo"
        v-on:update-todo="updateTodo"
        v-for="todo in todos"
        :todo=todo
        :key=todo.id
      />
    </div>
    <div class="no-todo" v-if="todos.length === 0 && !loading">
      <h4>GOOD JOB</h4>
      <p>You don't have anything todo!</p>
    </div>
    <div class="loader" v-if="loading">
      <div></div>
      <div></div>
      <div></div>
    </div>
  </div>
</template>

<script>
import Claim from '@/components/Claim.vue';
import NewTodoInput from '@/components/NewTodoInput.vue';
import TodoItem from '@/components/TodoItem.vue';

import axios from 'axios';
import debounce from 'lodash.debounce';

const API = 'http://localhost:3000/api/v1';

export default {
  name: 'Landing',
  components: {
    Claim,
    NewTodoInput,
    TodoItem,
  },
  data() {
    return {
      newTodo: '',
      todos: [],
      loading: true
    };
  },
  methods: {
    fetchData: debounce(function () {
      this.loading = true;
      axios.get(`${API}/todos`)
        .then((response) => {
          this.loading = false;
          this.todos = response.data;
        })
        .catch((error) => {
          this.loading = false;
          console.log(error);
        });
    }, 500),
    deleteTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      axios.delete(`${API}/todos/${todo.id}`)
        .then(() => {
          this.todos.splice(todoIndex, 1);
        })
        .catch((error) => {
          console.log(error);
        });
    },
    updateTodo(todo) {
      axios.patch(
        `${API}/todos/${todo.id}`, {
          description: todo.description,
          done: todo.done,
          deadline: todo.deadline,
      }).then((response) => {
        console.log(response);
      }).catch((error) => {
        console.log(error);
      });
    },
    addTodo: debounce(function (description) {
      axios.post(`${API}/todos`, {
        description,
        done: false,
        deadline: new Date(),
      }).then((response) => {
        this.todos.push(response.data);
        this.newTodo = '';
      }).catch((error) => {
        console.log(error);
      });
    }, 500),
  },
  created() {
    this.fetchData();
  },
};
</script>

<style lang="scss" scoped>
  .wrapper {
    margin: 0;
    width: 100%;
  }

  .todosWrapper {
    max-width: 780px;
    display: flex;
    flex-direction: column-reverse;
    align-items: center;
    justify-content: stretch;
    padding: 0 30px 0 110px;
    margin: 30px auto 0;
    right: 40px;
    position: relative;
  }

  .no-todo {
    display: flex;
    position: relative;
    margin: 70px auto 0;
    height: 100px;
    width: 300px;
    justify-content: center;
    align-items: center;
    flex-direction: column-reverse;
    background: white;
    border-radius: 5px;
    border-bottom: 1px solid #BDBDBD;

    h4 {
      margin-top: 5px;
      font-size: 20px;
    }
  }

  .loader {
    display: flex;
    position: relative;
    margin: 70px auto 0;
    height: 64px;
    width: 64px;
    justify-content: center;
    align-items: center;
  }
  .loader div {
    display: inline-block;
    position: absolute;
    left: 6px;
    width: 13px;
    background: #455A64;
    animation: loader 1.2s cubic-bezier(0, 0.5, 0.5, 1) infinite;
  }
  .loader div:nth-child(1) {
    left: 6px;
    animation-delay: -0.24s;
  }
  .loader div:nth-child(2) {
    left: 26px;
    animation-delay: -0.12s;
  }
  .loader div:nth-child(3) {
    left: 45px;
    animation-delay: 0;
  }
  @keyframes loader {
    0% {
      top: 6px;
      height: 51px;
    }
    50%, 100% {
      top: 19px;
      height: 26px;
    }
  }

</style>
