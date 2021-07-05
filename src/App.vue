<template>
  <div class="container mt-4">
    <div class="card">
      <div class="card-body">
        <div class="row">
          <div class="col">
            <h5 class="card-title">Simple Todo</h5>
          </div>

          <div class="col-auto">
            <small>Total : {{ totalTodo }}</small>
          </div>

          <hr>

          <div class="row">
            <div class="col-10">
              <input type="text" v-model="todo" @keyup.enter="addTodo" class="form-control" />
            </div>
            <div class="col-2">
              <button class="btn btn-primary" @click="addTodo">Add</button>
            </div>
          </div>

          <list-compnent :todos="list" @delTodo="delTodo" @doneTodo="doneTodo" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import { ref, toRefs, reactive, onMounted, computed } from "vue";
  import ListCompnent from "./components/List.vue";

  export default {
    setup() {
      const todo = ref('');
      const todos = reactive({
        list: [],
      });

      onMounted(() => {
        const items = localStorage.getItem('todos');

        // todos.list = JSON.parse(localStorage.getItem('todos'));
        todos.list = items ? JSON.parse(items) : [];
      });

      const totalTodo = computed(() => {
        return todos.list.length;
      });

      const addTodo = () => {
        if (todo.list != '') {
          todos.list.unshift({
            activity: todo.value,
            isDone: false
          });

          todo.value = "";
          saveToLocalStorage();
        }
      }

      const delTodo = (todoIndex) => {
        todos.list = todos.list.filter((item, index) => {
          if (index != todoIndex) {
            return item
          }
        });

        saveToLocalStorage();
      }

      const doneTodo = (todoIndex) => {
        todos.list = todos.list.filter((item, index) => {
          if (index == todoIndex) {
            item.isDone = true
          }

          return item;
        });

        saveToLocalStorage();
      }

      const saveToLocalStorage = () => {
        localStorage.setItem('todos', JSON.stringify(todos.list));
      }

      return { todo, ...toRefs(todos), totalTodo, addTodo, delTodo, doneTodo };
    },

    // data() {
    //   return {
    //     todo: "",
    //     todos: []
    //   }
    // },

    // mounted() {
    //   this.todos = JSON.parse(localStorage.getItem('todos'));
    // },

    // methods: {
    //   addTodo() {
    //     if (this.todo != '') {
    //       // this.todos.push(this.todo);

    //       this.todos.unshift({
    //         activity: this.todo,
    //         isDone: false
    //       });
    //       this.todo = "";
    //     }
    //     this.saveToLocalStorage();
    //   },
    //   delTodo(todoIndex) {
    //     this.todos = this.todos.filter((item, index) => {
    //       if (index != todoIndex) {
    //         return item;
    //       }
    //     });

    //     this.saveToLocalStorage();
    //   },
    //   doneTodo(todoIndex) {
    //     this.todos = this.todos.filter((item, index) => {
    //       if (index == todoIndex) {
    //         item.isDone = true
    //       }

    //       return item;
    //     });

    //     this.saveToLocalStorage();
    //   },
    //   saveToLocalStorage() {
    //     localStorage.setItem('todos', JSON.stringify(this.todos)); // save to local storage
    //   }
    // },

    components: { ListCompnent }
  }
</script>