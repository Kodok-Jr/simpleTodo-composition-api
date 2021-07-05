<template>
  <div>Count : {{ nilai }}</div>
  <button @click="add">Add</button>
</template>

<script>
  import { ref, reactive, toRefs, watchEffect } from "vue";

  export default {
    setup() {
      const counter = reactive({
        nilai: 0,
        foo: 'bar'
      });

      const add = () => {
        counter.nilai++;
      }

      watchEffect(() => {
        console.log(counter.nilai);
        // console.log(counter.bar);
      }, {
        // onTrigger(e) {
        //   console.log(e);
        // },
        onTrack(e) {
          console.log(e);
        },
      });

      return {
        // counter,
        ...toRefs(counter),
        add,
      }
    }
  }
</script>