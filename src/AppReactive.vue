<template>
  <div>{{ message }}</div>

  <hr>

  <pre>{{ user }}</pre>

  <hr>

  <!-- <p>Name : {{ user.name }}</p>
  <p>Age : {{ user.age }}</p> -->

  <hr>

  <p>Name : {{ name }}</p>
  <p>Age : {{ age }}</p>
</template>

<script>
  import { ref, reactive, toRefs } from "vue";

  export default {
    setup() {
      const message = ref('Halloo');

      const user = reactive({
        name: 'Kodok Junior',
        age: '35'
      });

      setTimeout(() => {
        // message.value = 'composition api';
        user.name = 'Hellndraz'
      }, 2000);

      return {
        message,
        // user
        ...toRefs(user),
      }
    }
  }
</script>