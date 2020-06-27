<template>
  <div class="todo-app">
    <h1>
      Todo
    </h1>
    <input type="text" class="new-todo" placeholder="enter to-do list" v-model="newTodo" @keyup.enter="addTodo">
    <div class="main">
      <div class="todo-list">
        <div class="todo" v-for="todo in TodoFilter" :class="{completed: todo.completed}">
          <input class="styled-checkbox" type="checkbox" v-model="todo.completed" style="border-radius: 8px">
          <div class="view" :class="{completed: todo.completed}">
            {{todo.name}}
          </div>
          <div class="remove-item" @click.prevent="removeTodo(todo)">
            &times;
          </div>
        </div>
      </div>
    </div>
    <div class="extra-container">
      <div class="check-all">
        <label>
        <input type="checkbox" :checked="!anyRemaining" @change="checkAllTodos">
          Check all
        </label>
      </div>
      <div class="remaining">
        <strong>
          {{remaining}}
        </strong>
        number of tasks
      </div>
    </div>
    <div class="extra-container">
      <button :class="{selected: filter === 'all'}" @click="filter = 'all'">
        All
      </button>
      <button :class="{selected: filter === 'make'}" @click="filter = 'make'">
        Make
      </button>
      <button :class="{selected: filter === 'completed'}" @click="filter = 'completed'">
        Completed
      </button>
    </div>
  </div>
</template>

<script>
  export default {
    name: "Todo",
    data() {
      return {
        todos: [],
        newTodo: '',
        filter: 'all'
      }
    },
    methods: {
      addTodo() {
        this.todos.push({
          completer: false,
          name: this.newTodo
        })
        this.newTodo = ''
      },
      removeTodo(todo) {
        this.todos = this.todos.filter(i => i !== todo)
      },
      checkAllTodos() {
        this.todos.forEach((todo) => todo.completed = event.target.checked)
      }
    },
    computed: {
      remaining() {
        return this.todos.filter(todo => !todo.completed).length
      },
      anyRemaining() {
        return this.remaining !== 0
      },
      TodoFilter() {
        if (this.filter === 'all') {
          return this.todos
        } else if (this.filter === 'make') {
          return this.todos(todo => !todo.completed)
        } else if (this.filter === 'completed') {
          return this.todos(todo => todo.completed)
        }
        return this.todos
      }
    },
  }
</script>

<style scoped>
  h1 {
    font-family: 'Monoton', cursive;
    font-size: 45px;
    padding-left: 50px;
  }

  .todo-app {
    display: flex;
    align-content: center;
    flex-direction: column;
    border: 3px cornflowerblue solid;
    margin: 70px 500px;
    padding-left: 60px;
    padding-top: 30px;
    font-family: 'Cormorant Garamond', serif;
    font-size: 20px;
    word-wrap: break-word;
  }


  .new-todo {
    border: none;
    margin-top: 50px;
    margin-right: 50px;
    border-bottom: 1px solid black;
  }

  .todo {
    list-style: none;
    text-decoration: blink;
  }


  .check-all {
    font-family: 'Abril Fatface', sans-serif;
    font-size: 15px;
    -webkit-appearance: none;
    appearance: none;
  }

  .remove-item {
    cursor: pointer;
    display: flex;
    margin-left: 80%;
    margin-top: -30px;

    &:hover {
      color: black;
    }
  }

  .remaining {
    font-family: 'Abril Fatface', sans-serif;
    font-size: 15px;
  }

  .extra-container {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding-top: 40px;
    margin-bottom: 15px;
    margin-right: 20px;
    font-size: 15px;
  }

  button {
    background-color: white;
    border: none;
  }

  .view {
    margin-top: -33px;
    margin-left: 50px;
  }

  /*.todo-bar {*/
  /*  font-size: 17px;*/
  /*  list-style: none;*/
  /*  display: flex;*/
  /*  margin: 10px -10px;*/
  /*}*/

  .completed {
    text-decoration: line-through;
    color: black;
  }


</style>
