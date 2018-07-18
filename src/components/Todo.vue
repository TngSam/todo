<template>
  <div id="app">
    <div class="to-do">
      <h1 class="to-do__title">To-Do</h1>
      <ol class="to-do__list">
        <li class="to-do__list__item" v-for="todo in todos" :key='todo.id'>
          <div class="to-do__list__item__text">{{ todo.text }}</div>
          <div class="to-do__list__item__actions">
            <img src="@icon/font-awesome/icons/check.svg" height="26" width="26" 
              class="to-do__list__item__actions_done" @click="doneTodo(todo.id)" />
            <img src="@icon/font-awesome/icons/pencil.svg" height="26" width="26"
              class="to-do__list__item__actions_edit" @click="editTodo(todo.id)" />
            <img src="@icon/font-awesome/icons/times.svg" height="26" width="26"
              class="to-do__list__item__actions_remove" @click="removeTodo(todo.id)" />
          </div>
        </li>
      </ol>
      <div class="to-do__add">
        <input class="to-do__add__text" type="text" v-model='todoText' id='addTodo'>
        <div class="to-do__add__button">
          <img src="@icon/font-awesome/icons/plus.svg"
            @click="addTodo" height="26" width="26" />          
        </div>
      </div>
    </div>
    <div class="done">
      <h1 class="done__title">Done</h1>
      <ul class="done__list">
        <li class="done__list__item" v-for="todo in done" :key="todo.id">
          {{ todo.text }}
        </li>
      </ul>
    </div>    
  </div>
</template>

<script lang="ts">
  import * as $ from 'jquery';
  import { Component, Vue, Prop } from 'vue-property-decorator';

  @Component
  export default class Todo extends Vue {
    private todos: any[] = [];
    private done: any[] = [];
    private todoText: string = '';

    private addTodo() {
      this.todos.push({
        id: this.todos.length + 1,
        text: this.todoText,
      });
      this.todoText = '';
    }
    private doneTodo(id: number) {
      this.todos = this.todos.filter((todo: any) => {
        if (todo.id !== id) {
          return true;
        }
        this.done.unshift(todo);
      });
    }
    private editTodo(id: number) {
      const $todo = $($('.to-do__list__item__text')[id - 1]);
      $todo.toggleClass('contenteditable');
      $todo.prop('contenteditable', $todo.hasClass('contenteditable')).focus();
      this.todos[id - 1].text = $todo.text();
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
  * {
    box-sizing: border-box;
    padding: 0;
    margin: 0;
  }
  ul {
    list-style-type: none;
  }
  input {
    outline: none;
  }
  #app {
    padding-top: 40px;
    font-family: 'Helvetica';
    display: flex;
    justify-content: center;
  }
  .to-do {
    height: 400px;
    max-height: 400px;
    width: 400px;
    text-align: center;
    border: 1px solid green;
    padding-top: 20px;
    margin-right: 20px;
    position: relative;
    overflow-y: scroll;
    .to-do__add {
      width: 100%;
      height: 35px;
      position: absolute;
      bottom: 0;
      left: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      .to-do__add__text {
        padding: 5px 10px;
        font-size: 1.05rem;
        border: none;
        border-top: 1px solid black;
        border-right: 1px solid black;
        width: 92%;
        height: 35px;
        display: block;
      }
      .to-do__add__button {
        width: 8%;
        height: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        border-top: 1px solid black;
      }
    }
    .to-do__list {
      .to-do__list__item {
        padding: 10px;
        width: 100%;
        border-top: 1px solid black;
        border-left: none;
        border-right: none;
        display: flex;
        align-items: center;
        justify-content: space-between;
        &:first-child {
          margin-top: 15px;
        }
        &:last-child {
          border-bottom: 1px solid black;
          margin-bottom: 15px;
        }
        .to-do__list__item__text {
          margin-right: 20px;
          font-size: 1.25rem;
        }
        .to-do__list__item__actions img {
          margin: 0 4px;
        }
      }
    }
  }
  .done {
    height: 400px;
    max-height: 400px;
    width: 400px;
    text-align: center;
    border: 1px solid green;
    padding: 20px 0;
    margin-left: 20px;
    overflow-y: scroll;
    .done__list {
      .done__list__item {
        padding: 10px 20px;
        width: 100%;
        border: 1px solid #999;
        border-left: none;
        border-right: none;
        text-align: left;
        font-size: 1.25rem;
        color: #999;
        &:first-child {
          margin-top: 15px;
        }
      }
    }
  }
</style>