<template>
  <!-- <div>Count : {{ counter }}</div> -->

  <div>Count : {{ nilai }}</div>
  <button @click="add">Add</button>

  <div>Result : {{ result }}</div>
</template>

<script>
  import { ref, reactive, toRefs, computed } from "vue";

  export default {
    setup() {
      // const counter = ref(0);
      const counter = reactive({
        nilai: 0
      });

      const addNum = ref(1);

      const add = () => {
        result.value = 5;

        // counter.value++
        counter.nilai++;
      }

      // const result = computed(() => counter.nilai + addNum.value);

      const result = computed({
        get: () => counter.nilai + addNum.value,
        set: (val) => (addNum.value = val)
      }); // menggunakan setter & getter

      return {
        // counter,
        ...toRefs(counter),
        add,
        result
      }
    }
  }
</script>