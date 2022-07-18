<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div>
      <label for="">Name</label>
      <input type="text" v-model="todo.name" />
      <label for="">Email</label>
      <input type="text" v-model="todo.email" />
      <button @click="storeTodo">{{ isEditing ? "Update" : "Save" }}</button>
    </div>
    <div>
      <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>Name</th>
            <th>Email</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(todo, index) in todos" :key="todo">
            <td>{{ index + 1 }}</td>
            <td>{{ todo.name }}</td>
            <td>{{ todo.email }}</td>
            <td>
              <button @click="editTodo(index)">Edit</button>
              <button @click="removeTodo(index)">Delete</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      isEditing: false,
      todo: [],
      todos: [],
      selectedTodo: null,
    };
  },
  methods: {
    storeTodo() {
      if (this.todo !== "") {
        if (this.isEditing) {
          this.todos[this.selectedTodo] = this.todo;
          this.isEditing = false;
          this.todo = [];
        } else {
          this.todos.push(this.todo);
          this.todo = [];
        }
      }
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
    editTodo(index) {
      this.isEditing = true;
      this.todo.name = this.todos[index].name;
      this.todo.email = this.todos[index].email;
      this.selectedTodo = index;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
