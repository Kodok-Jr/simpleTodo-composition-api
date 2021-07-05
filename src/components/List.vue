<template>
  <div class="mt-4">
    <ul class="list-group">
      <li class="list-group-item" v-for="(todo, index) in todos" :key="index">
        <div class="row">
          <div class="col">
						<span v-if="todo.isDone"><del>{{ todo.activity }}</del></span>
						<span v-else>{{ todo.activity }}</span>
					</div>
          <div class="col-auto">
            <button @click="doneTodo(index)" class="btn btn-sm btn-success">&#10003;</button>
          </div>
          <div class="col-auto">
            <button @click="delTodo(index)" class="btn btn-sm btn-danger">x</button>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
	export default {
		props: {
			todos: {
				type: Array,
				default: []
			}
		},

		setup(props, { emit }) {
			const delTodo = (index) => {
				emit('delTodo', index);
			}

			const doneTodo = (index) => {
				emit('doneTodo', index);
			}

			return { delTodo, doneTodo }
		},

		// methods: {
		// 	delTodo(index) {
		// 		this.$emit('delTodo', index);
		// 	},
		// 	doneTodo(index) {
		// 		this.$emit('doneTodo', index);
		// 	}
		// }
	};
</script>