<template>
  <user-component :label="label" :user="user" blablabla="testing" @submit="onSubmit">
    <div>ini slot</div>
  </user-component>

  <button @click="changeNmae">Change</button>
</template>

<script>
  import { ref, reactive } from "vue";
  import UserComponent from "./components/User.vue";

  export default {
     emits: ["onSubmit"],
    setup() {
      const label = ref('Biodata');
      const user = reactive({
        name: "Kodok Junior",
        age: 35
      });

      const changeNmae = () => {
        user.name = 'Dadang Durugdug'
      }

      const onSubmit = (val) => {
        console.log(val);
      }

      return {
        label, user, changeNmae, onSubmit
      }
    },
    components: { UserComponent }
  }
</script>