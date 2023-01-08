<template>
  <div id="app">
    <input type="text" v-model="newTodoItem" @keydown="addTodo" />
    <!-- data - props - property(속성): 변수(자식컴포넌트에서 사용할)="데이터" -->
    <!-- <add-todo :placeholder="placeholder" v-on:emit-add-todo="emitAddTodo"></add-todo> -->

    <todo-list v-bind:todo-list="todoList" v-on:delete-todo="deleteTodo"></todo-list>

    <!-- <table>
      <thead>
        <tr>
          <th>NO.</th>
          <th>TODO</th>
          <th>DONE</th>
          <th>EDIT</th>
          <th>DELETE</th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="(todo, index) in todoList" :key="'todo_' + todo.id">
          <td>{{ todo.id }}</td>

          <td v-if="todo.isEdit === false">{{ todo.todo }}</td>
          <td v-else>
            <input type="text" :placeholder="todo.todo" v-model="editTodoItem" @keydown="editTodoText($event, index)" />
          </td>

          <td @click="toggleStatus(index)">{{ todo.isCompleted }}</td>
          <td><button @click="editTodo(index)">EDIT</button></td>
          <td><button @click="deleteTodo(index)">DELETE</button></td>
        </tr>
      </tbody>
    </table> -->
  </div>
</template>

<script>
// import AddTodo from "./components/AddTodo.vue";
import TodoList from "./components/TodoList.vue";

export default {
  name: "App",

  components: {
    // AddTodo,
    TodoList,
  },

  data() {
    return {
      newTodoItem: "",
      editTodoItem: "",

      placeholder: "test",

      todoList: [
        {
          id: 1,
          todo: "Study javascript",
          isCompleted: false,
          isEdit: false,
        },
        {
          id: 2,
          todo: "Do Homework",
          isCompleted: false,
          isEdit: false,
        },
        {
          id: 3,
          todo: "Take a shower",
          isCompleted: false,
          isEdit: false,
        },
        {
          id: 4,
          todo: "Brush Teeth",
          isCompleted: false,
          isEdit: false,
        },
        {
          id: 5,
          todo: "Talk to friend",
          isCompleted: false,
          isEdit: false,
        },
      ],
    };
  },

  methods: {
    emitAddTodo(data) {
      console.log("parent", "emit add todo", data);
      data.id = this.todoList[this.todoList.length - 1].id + 1;
      this.todoList.push(data);
    },
    toggleStatus(index) {
      if (this.todoList[index].isCompleted) {
        this.todoList[index].isCompleted = false;
      } else {
        this.todoList[index].isCompleted = true;
      }
    },

    addTodo(e) {
      if (e.keyCode === 13) {
        let newTodoObj = {
          id: this.todoList[this.todoList.length - 1].id + 1,
          todo: this.newTodoItem,
          isCompleted: false,
          isEdit: false,
        };

        this.todoList.push(newTodoObj);
        this.newTodoItem = "";
      }
    },

    deleteTodo(index) {
      console.log("-----------Parent: delete todo");
      this.todoList.splice(index, 1);
    },

    editTodo(index) {
      console.log("index", index);
      this.todoList[index].isEdit = !this.todoList[index].isEdit;
    },

    editTodoText(e, index) {
      if (e.keyCode === 13) {
        this.todoList[index].todo = this.editTodoItem;
        this.todoList[index].isEdit = !this.todoList[index].isEdit;
        this.editTodoItem = "";
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

table thead tr th {
  height: 30px;
  background-color: black;
  color: white;
}

table thead tr th:nth-child(2) {
  width: 150px;
}

table tbody tr {
  height: 30px;
}

/* odd - 홀수 / even - 짝수 */
table tbody tr:nth-child(odd) {
  background-color: #cccccc;
}

table tbody tr:hover {
  background-color: lightgreen;
}

input {
  margin-bottom: 20px;
  padding: 10px;
  font-size: 14px;
  border-radius: 10px;
  border: 1px solid lightgray;
}
</style>
