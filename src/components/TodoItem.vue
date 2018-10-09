<template>
  <div v-bind:class="['todoWrapper', {done: todo.done}]">
    <div class="deadline">
      <p class="time">{{ todo.deadline | moment("H:m") }}</p>
      <p class="date">{{ todo.deadline | moment("d.M.YYYY") }}</p>
    </div>
    <div v-bind:class="['todo']">
      <div
        v-bind:class="['state first-plan', {complete: todo.done}]"
        v-on:click="updateTodo"
      >
        <dir class='done-marker'></dir>
      </div>

      <p class="first-plan">
        {{ todo.description }}
      </p>
      <a class="delete first-plan" v-on:click="deleteTodo(todo)"></a>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TodoItem',
  props: {
    todo: {
      type: Object,
      required: true,
    },
  },
  methods: {
    deleteTodo(todo) {
      this.$emit('delete-todo', todo);
    },
    updateTodo() {
      this.todo.done = !this.todo.done;
      this.$emit('update-todo', this.todo);
    },
  },
};
</script>

<style lang="scss" scoped>
  .todoWrapper {
    display: flex;
    width: 740px;
    right: 50px;
    position: relative;
  }

  .done {
    .todo {
      color: white;

      &:after {
        padding: 900px;
      }
    }
    .deadline {
      // color: #CFD8DC;

      p {
        right: -70px;
      }
    }
  }

  .todo {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    margin: 0 0 5px 0;
    width: 700px;
    padding: 0 10px;
    box-shadow: 0px 2px 5px -1px rgba(0, 0, 0, 0.25);
    position: relative;
    overflow: hidden;
    transition: color .32s;
    background: white;
    border-radius: 5px;

    &:after {
      content: '';
      position: absolute;
      padding: 0;
      display: block;
      background: #607D8B;
      left: -42px;
      z-index: 1;
      border-radius: 100%;
      transition: padding .5s;
    }
  }

  .deadline {
    width: 110px;
    display: flex;
    flex-direction: column;
    text-align: right;
    padding: 12px;
    color: #3f5b65;
    transition: color .3s;
    overflow: hidden;

    p {
      transition: right .3s;
      right: 0;
      width: 100%;
      margin: 0 auto;
      position: relative;

      &.date {
        font-size: 12px;
      }

      &.time {
        font-size: 14px;
        font-weight: 600;
      }
    }
  }

  .first-plan {
    z-index: 100;
  }

  .state {
    width: 30px;
    height: 30px;
    color: white;
    border: none;
    position: relative;
    transition: box-shadow .3s, background .3s;
    border-radius: 5px;
    cursor: pointer;
    border: 1px solid #4c7f8e;
    position: relative;

    .done-marker {
      margin: 0 auto;
      opacity: 0;
      background: transparent;
      display: block;
      border-radius: 3px;
      top: 0;
      bottom: 0;
      left: 0;
      right: 0;
      position: relative;
      padding: 14px;
      overflow: hidden;
      transition: opacity .3s;

      &:hover {
        opacity: .4;
      }

      &:before, &:after {
        content: "";
        background: #8BC34A;
        width: 3px;
        z-index: 2;
        display: block;
        position: absolute;
        margin: auto;
        top: 25%;
        border: 25%;
        transition: transform .3s;
      }

      &:before {
        transform: rotate(45deg);
        left: 0;
        right: -14%;
        top: 28%;
        height: 50%;
      }

      &:after {
        transform: rotate(-30deg);
        left: 0;
        right: 29%;
        top: 43%;
        height: 30%;
      }
    }

    &.complete {
      .done-marker {
        opacity: 1;
      }
    }
  }

  .delete {
    width: 30px;
    height: 30px;
    background: #455A64;
    color: white;
    box-shadow: 0px 2px 5px -1px rgba(0, 0, 0, 0.25);
    border: none;
    position: relative;
    transition: box-shadow .3s, background .3s;
    border-radius: 5px;
    cursor: pointer;

    &:before, &:after {
      content: "";
      background: white;
      width: 2px;
      z-index: 2;
      height: 50%;
      display: block;
      position: absolute;
      left: 25%;
      right: 25%;
      margin: auto;
      top: 25%;
      border: 25%;
      transition: transform .3s;
    }

    &:before {
      transform: rotate(90deg)
    }

    &:after {
      transform: rotate(90deg)
    }

    &:hover {
      box-shadow: 0px 2px 8px -1px rgba(0, 0, 0, 0.75);
      background: red;

      &:after {
        transform: rotate(45deg)
      }
      &:before {
        transform: rotate(135deg)
      }
    }
  }
</style>
