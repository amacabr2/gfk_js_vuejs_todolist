<template>

    <section class="todoapp">

        <header class="header">
            <h1>Todos</h1>
            <input type="text" class="new-todo" placeholder="Ajouter une tache" v-model="newTodo" @keyup.enter="addTodo">
        </header>

        <div class="main">
            <ul class="todo-list">
                <li class="todo" v-for="todo in todos" :class="{completed: todo.completed}">
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
                <li><a class="selected" href="#">Toutes</a></li>
                <li><a href="#">A faires</a></li>
                <li><a href="#">Faites</a></li>
            </ul>
        </footer>

    </section>

</template>

<script>
    /* eslint-disable space-before-function-paren,no-multiple-empty-lines,no-trailing-spaces */

    export default {

      data() {
        return {
          todos: [{
            name: 'Tache de test',
            completed: false
          }],
          newTodo: ''
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
        }
      }

    }
</script>

<style src="./todos.css"></style>
