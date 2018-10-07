<template>
  <div v-bind:class="['newTodoWrapper', {typing: value.length > 0 }]">
    <div class="descriptionInput">
      <div class="enter">ENTER</div>
      <input
        id="descriptionInput"
        name="descriptionInput"
        v-model="value"
        @keyup="handleChange"
        placeholder="Add new Todo"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: 'NewTodoInput',
  props: {
    value: {
      type: String,
      required: true,
    },
  },
  methods: {
    handleChange(e) {
      if (e.keyCode === 13) {
        this.value = null;
        this.$emit('create-todo', e.target.value);
      }
    },
  },
};
</script>

<style lang="scss" scoped>

  .newTodoWrapper.typing {
    input {
      padding-right: 70px;
    }

    .enter {
      right: 8px;
    }
  }

  .descriptionInput {
    margin: 20px 30px 0;
    display: flex;
    flex-direction: column;
    width: 640px;
    position: relative;
    overflow: hidden;

    .enter {
      transition: right .5s;
      content: 'ENTER';
      position: absolute;
      padding: 5px;
      display: block;
      background: white;
      border: 1px solid #BDBDBD;
      right: -65px;
      top: 10px;
      z-index: 1;
      border-radius: 5px;
      transition: right .5s;
      font-size: 12px;
    }

    input {
      padding: 10px;
      height: 49px;
      border: 0;
      border-bottom: 1px solid #BDBDBD;
      color: #757575;
      text-align: center;
      transition: box-shadow .3s easy-out;
      font-size: 18px;
      font-weight: 300;
      transition: padding-right .5s;
      border-radius: 5px;

      &:focus {
        outline: none;
        box-shadow: 0 10px 20px -8px rgba(#BDBDBD, .5);
      }
    }
  }
  .newTodoWrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 0;
    width: 100%;
  }
</style>
