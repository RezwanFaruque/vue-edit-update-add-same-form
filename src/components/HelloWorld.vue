<template>
  <div>
    <form @submit.prevent="addtodos">
      <input type="text" v-model="title" />
      <button type="submit">Add Todo</button>
    </form>
    <div>
      <table>
        <tr v-for="todo in todos" :key="todo.id">
          <td v-show="!todo.isedit">{{ todo.title }}</td>
          <td v-show="todo.isedit">
            <input type="text" v-model="todo.title" />
          </td>
          <td v-show="todo.isedit">
            <button @click.prevent="updatetodo(todo)">Update</button>
          </td>
          <td v-show="!todo.isedit">
            <button @click.prevent="edittodos(todo)">Edit</button>
          </td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",

  data: function () {
    return {
      todos: [
        {
          title: "Todo title",
          isedit: false,
        },
      ],
      title: "",
    };
  },

  computed: {},

  methods: {
    addtodos() {
      this.todos.push({
        title: this.title,
        isedit: false,
      });

      this.title = "";
    },

    edittodos(todo) {
      todo.isedit = true;
    },

    updatetodo(todo) {
      let update = {
        title: todo.title,
        isedit: false,
      };
      this.$set(this.todos, todo.id, update);

      todo.isedit = false;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
