<template>

    <section class="todoapp">

        <header class="header">
            <h1>Todos</h1>
            <input type="text" class="new-todo" placeholder="Ajouter une tache" v-model="newTodo" @keyup.enter="addTodo">
        </header>

        <div class="main">

            <input type="checkbox" class="toggle-all" v-model="alldone">

            <ul class="todo-list">
                <li class="todo" v-for="todo in filteredTodos" :class="{completed: todo.completed}">
                    <div class="view">
                        <input type="checkbox" v-model="todo.completed" class="toggle">
                        <label>{{ todo.name }}</label>
                    </div>
                </li>
            </ul>

        </div>

        <footer class="footer">
            <span class="todo-count"><strong>{{ remaining }}</strong> tâche(s) à faire</span>
            <ul class="filters">
                <li><a :class="{selected: filter === 'all'}" @click.prevent="filter = 'all'">Toutes</a></li>
                <li><a :class="{selected: filter === 'todo'}" @click.prevent="filter = 'todo'">A faires</a></li>
                <li><a :class="{selected: filter === 'done'}" @click.prevent="filter = 'done'">Faites</a></li>
            </ul>
        </footer>

    </section>

</template>

<script>
    /* eslint-disable space-before-function-paren,no-multiple-empty-lines,no-trailing-spaces */

    export default {

      data() {
        return {
          alldone: false,
          todos: [],
          newTodo: '',
          filter: 'all'
        }
      },

      methods: {
        addTodo() {
          this.todos.push({
            completed: false,
            name: this.newTodo
          })
          this.newTodo = ''
        }
      },

      computed: {
        remaining() {
          return this.todos.filter(todo => !todo.completed).length
        },
        filteredTodos() {
          if (this.filter === 'todo') {
            return this.todos.filter(todo => !todo.completed)
          } else if (this.filter === 'done') {
            return this.todos.filter(todo => todo.completed)
          }
          return this.todos
        }
      }

    }
</script>

<style src="./todos.css"></style>
