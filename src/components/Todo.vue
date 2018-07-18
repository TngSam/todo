<template>
  <div id="app">
    <div class="to-do">
      <h1 class="to-do__title">To-Do</h1>
      <ol class="to-do__list">
        <li class="to-do__list__item" v-for="todo in todos" :key='todo.id'>
          <div class="to-do__list__item__text" v-model='todo.text'></div>
          <div class="to-do__list__item__actions">
            <div class="to-do__list__item__actions_done" @click="doneTodo(todo.id)">Done</div>
            <div class="to-do__list__item__actions_edit" @click="editTodo(todo.id)">Edit</div>
            <div class="to-do__list__item__actions_remove" @click="removeTodo(todo.id)">Remove</div>
          </div>
        </li>
      </ol>
      <div class="done">
        <h1 class="done__title">Done</h1>
        <ul class="done__list">
          <li v-for="todo in done" :key="todo.id">
            {{ todo.text }}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
  import { $ } from 'jquery';
  import { Component, Vue, Prop } from 'vue-property-decorator';

  @Component
  export default class Todo extends Vue {
    private todos: any[] = [];
    private done: any[] = [];

    private doneTodo(id: number) {
      this.todos = this.todos.filter((todo: any) => {
        if (todo.id !== id) {
          return true;
        }
        this.done.unshift(todo);
      });
    }
    private editTodo(id: number) {

    }
    private removeTodo(id: number) {
      this.todos = this.todos.filter((todo: any) => {
        if (todo.id !== id) {
          return true;
        }
      });
    }
  }
</script>

<style scoped lang="scss">
  #app {
    font-family: 'Helvetica';
  }
</style>