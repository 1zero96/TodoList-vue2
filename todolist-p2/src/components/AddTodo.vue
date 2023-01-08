<template>
  <input type="text" v-model="newTodoItem" @keydown="addTodo" :placeholder="placeholder" />
</template>

<script>
export default {
  name: "AddTodo",

  props: {
    placeholder: {
      type: String,
      default() {
        return "";
      },
    },
  },

  data() {
    return {
      newTodoItem: "",
    };
  },
  methods: {
    addTodo(e) {
      if (e.keyCode === 13) {
        let newTodoObj = {
          todo: this.newTodoItem,
          isCompleted: false,
          isEdit: false,
        };

        // this.$emit('메소드 이름', 부모에게 보내줄 테이터)
        this.$emit("emit-add-todo", newTodoObj);

        this.newTodoItem = "";
      }
    },
  },
};
</script>
