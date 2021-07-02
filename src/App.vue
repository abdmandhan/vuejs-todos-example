<template>
  <div class="container">
    <div>Contoh VueJS</div>
    <div>Total Todos {{ totalTodos }}</div>

    <div class="todos">
      <ul v-for="item in todos" :key="item.id">
        <li>
          <span v-if="edit_id !== item.id">
            {{ item.name }}
          </span>
          <input
            v-else-if="edit_id === item.id"
            type="text"
            v-model="todo.name"
          />
          <button @click="remove(item.id)">remove</button>
          <button @click="edit(item.id)" v-if="edit_id !== item.id">
            edit
          </button>
          <button @click="update(item.id)" v-else>update</button>
        </li>
      </ul>
    </div>
    <div v-if="!edit_id">
      <div class="form-control">
        <span class="label">Name:</span>
        <span class="input">
          <input type="text" v-model="todo.name" />
        </span>
      </div>
      <button @click="add">Add</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      edit_id: null,
      todo: {
        name: null,
      },
      todos: [
        {
          id: 1,
          name: "Todo 1",
        },
        {
          id: 2,
          name: "Todo 2",
        },
      ],
    };
  },
  methods: {
    add() {
      if (this.todo.name) {
        this.todos.push({
          id: Math.random(),
          ...this.todo,
        });

        this.todo = {
          name: "",
        };
      } else {
        alert("todo name null");
      }
    },
    remove(id) {
      this.todos = this.todos.filter((a) => a.id !== id);
    },
    edit(id) {
      this.edit_id = id;
      this.todo = this.todos.find((a) => a.id == id);
    },
    update(id) {
      this.todos = this.todos.map((a) => (a.id == id ? this.todo : a));
      this.edit_id = null;
      this.todo = {
        name: "",
      };
    },
  },
  computed: {
    totalTodos() {
      return this.todos.length;
    },
  },
};
</script>

<style>
.container {
  width: 100%;
}

.form-control {
  display: inline;
}
</style>
