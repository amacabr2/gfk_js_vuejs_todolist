<template>

    <section class="todoapp">

        <header class="header">
            <h1>Todos</h1>
            <input type="text" class="new-todo" placeholder="Ajouter une tache" v-model="newTodo" @keyup.enter="addTodo">
        </header>

        <div class="main">
            <ul class="todo-list">
                <li class="todo" v-for="todo in todos">
                    <div class="view">
                        <input type="checkbox" v-model="todo.completed" class="toggle">
                        <label>{{ todo.name }}</label>
                    </div>
                </li>
            </ul>
        </div>

    </section>

</template>

<script>
    /* eslint-disable space-before-function-paren,no-multiple-empty-lines,no-trailing-spaces */

    export default {

      data() {
        return {
          todos: [{
            name: 'Tache de test',
            complete: false
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
      }

    }
</script>

<style src="./todos.css"></style>
