<template>
  <li class="todo" :class="{'label-default': todo.done, editing: editing}">
    <div>
      <input type="checkbox"
             class="toggle"
             :checked="todo.none"
             @change="toggleTodo({todo: todo})"/>

      <label v-text="todo.text"
             @dblclick="editing = true">
      </label>

      <button class="btn btn-xs btn-danger"
              @click="deleteTodo({todo: todo})">
        Eliminar
      </button>
    </div>

    <input class="edit form-control"
           v-show="editing"
           :value="todo.text"
           @keyup.enter="doneEdit"
           @keyup.esc="cancelEdit"
           @blur="doneEdit"/>
  </li>
</template>

<script>
  import { mapMutations } from 'vuex'
  export default {
    name: 'todo',
    props: ['todo'],
    data () {
      return {
        editing: false
      }
    },
    methods: {
      ...mapMutations([ // mapea 3 funciones de las que se habian definido en el archivo "components/todo.vue"
        'editTodo',
        'toggleTodo',
        'deleteTodo'
      ]),
      doneEdit (e) {
        const value = e.target.value.trim()
        const {todo} = this
        if (!value) {
          this.deleteTodo({
            todo
          })
        } else if (this.editing) {
          this.editTodo({
            todo, value
          })

          this.editing = false
        }
      },
      cancelEdit (e) {
        e.target.value = this.todo.text
        this.editing = false
      }
    }
  }
</script>
