<template>

    <section class="todoapp">

        <header class="header">
            <h1>Todos</h1>
            <input type="text" class="new-todo" placeholder="Ajouter une tache" v-model="newTodo" @keyup.enter="addTodo">
        </header>

        <div class="main">

            <input type="checkbox" class="toggle-all" v-model="allDone">

            <ul class="todo-list">
                <li class="todo" v-for="todo in filteredTodos" :class="{completed: todo.completed, editing: todo === editing}">
                    <div class="view">
                        <input type="checkbox" v-model="todo.completed" class="toggle">
                        <label @dblclick="editTodo(todo)">{{ todo.name }}</label>
                        <button class="destroy" @click.prevent="deleteTodo(todo)"></button>
                    </div>
                    <input type="text" class="edit" v-model="todo.name" @keyup.esc="cancelEdit" @keyup.enter="doneEdit" v-focus="todo === editing" @blur="doneEdit">
                </li>
            </ul>

        </div>

        <footer class="footer" v-show="hasTodos">
            <span class="todo-count"><strong>{{ remaining }}</strong> tâche(s) à faire</span>
            <ul class="filters">
                <li><a :class="{selected: filter === 'all'}" @click.prevent="filter = 'all'">Toutes</a></li>
                <li><a :class="{selected: filter === 'todo'}" @click.prevent="filter = 'todo'">A faires</a></li>
                <li><a :class="{selected: filter === 'done'}" @click.prevent="filter = 'done'">Faites</a></li>
            </ul>
            <button class="clear-completed" v-show="completed" @click.prevent="deleteCompleted">Supprimer tâches finies</button>
        </footer>

    </section>

</template>

<script>
    /* eslint-disable space-before-function-paren,no-multiple-empty-lines,no-trailing-spaces */

    import Vue from 'vue'

    export default {

      data() {
        return {
          todos: [],
          newTodo: '',
          filter: 'all',
          editing: null,
          oldTodo: ''
        }
      },

      methods: {

        addTodo() {
          this.todos.push({
            completed: false,
            name: this.newTodo
          })
          this.newTodo = ''
        },

        deleteTodo(todo) {
          this.todos = this.todos.filter(t => t !== todo)
        },

        deleteCompleted() {
          this.todos = this.todos.filter(todo => !todo.completed)
        },

        editTodo(todo) {
          this.editing = todo
          this.oldTodo = todo.name
        },

        doneEdit() {
          this.editing = null
        },

        cancelEdit() {
          this.editing.name = this.oldTodo
          this.doneEdit()
        }

      },

      computed: {

        allDone: {
          get() {
            return this.remaining === 0
          },
          set(value) {
            console.log(value)
            this.todos.forEach(todo => {
              todo.completed = value
            })
          }
        },

        remaining() {
          return this.todos.filter(todo => !todo.completed).length
        },

        completed() {
          return this.todos.filter(todo => todo.completed).length
        },

        filteredTodos() {
          if (this.filter === 'todo') {
            return this.todos.filter(todo => !todo.completed)
          } else if (this.filter === 'done') {
            return this.todos.filter(todo => todo.completed)
          }
          return this.todos
        },

        hasTodos() {
          return this.todos.length > 0
        }

      },

      directives: {
        focus(el, value) {
          if (value) {
            Vue.nextTick(_ => {
              el.focus()
            })
          }
        }
      }

    }
</script>

<style src="./todos.css"></style>
