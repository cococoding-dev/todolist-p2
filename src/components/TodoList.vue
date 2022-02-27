<template>
  <table>
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
      <tr v-for="(todo, index) in todoListA" :key="'todo_' + todo.id">
        <td>{{ todo.id }}</td>

        <td v-if="todo.isEdit === false">{{ todo.todo }}</td>
        <td v-else>
          <input
            type="text"
            :placeholder="todo.todo"
            v-model="editTodoItem"
            @keydown="editTodoText($event, index)"
          />
        </td>

        <td @click="toggleStatus(index)">{{ todo.isCompleted }}</td>
        <td><button @click="editTodo(index)">EDIT</button></td>
        <td><button @click="deleteTodo(index)">DELETE</button></td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: "TodoList",

  props: {
    todoListA: {
      type: Array,
      default() {
        return [];
      },
    },
  },

  data() {
    return {
      editTodoItem: "",

      //   todoList: [
      //     {
      //       id: 1,
      //       todo: "Study Javascript",
      //       isCompleted: false,
      //       isEdit: false,
      //     },
      //     {
      //       id: 2,
      //       todo: "Do Homework",
      //       isCompleted: false,
      //       isEdit: false,
      //     },
      //     {
      //       id: 3,
      //       todo: "Take a shower",
      //       isCompleted: false,
      //       isEdit: false,
      //     },
      //     {
      //       id: 4,
      //       todo: "Brush Teeth",
      //       isCompleted: false,
      //       isEdit: false,
      //     },
      //     {
      //       id: 5,
      //       todo: "Talk to mom",
      //       isCompleted: false,
      //       isEdit: false,
      //     },
      //   ],
    };
  },

  methods: {
    toggleStatus(index) {
      // this.todoList[index].isCompleted = !this.todoList[index].isCompleted

      if (this.todoListA[index].isCompleted) {
        this.todoListA[index].isCompleted = false;
      } else {
        this.todoListA[index].isCompleted = true;
      }
    },

    deleteTodo(index) {
      console.log("----child: delete todo");
      this.$emit("delete-todo", index);
      //   this.todoListA.splice(index, 1);
    },

    editTodo(index) {
      this.todoListA[index].isEdit = !this.todoListA[index].isEdit;
    },

    editTodoText(e, index) {
      if (e.keyCode === 13) {
        this.todoListA[index].todo = this.editTodoItem;
        this.todoListA[index].isEdit = !this.todoListA[index].isEdit;
        this.editTodoItem = "";
      }
    },
  },
};
</script>