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
  export default {

  }
</script>
