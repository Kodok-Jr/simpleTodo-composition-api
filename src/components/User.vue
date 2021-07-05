<template>
    <div>User Component</div>
    <hr>
    <!-- <p>{{ message }}</p> -->
    <!-- <br> -->
    <div>{{ label }} : {{ user.name }}</div>
    <div>{{ description }}</div>
    <button @click="submit">Submit</button>
    <hr>
    <slot/>
</template>

<script>
import { ref, toRefs, computed, onMounted } from "vue";

export default {
    props: {
        label: {
            type: String,
            default: ''
        },
        user: {
            type: Object,
            default: () => {}
        }
    },
    setup(props, { attrs, slots, emit }) {
        // const message = ref('ini adalah komponen');

        // return { message}

        // console.log(props); // tanpa destructure (toRefs)

        const { label, user } = toRefs(props);

        // console.log(user.value);

        const description = computed(() => {
            return `${label.value} : ${user.value.name}`
        });

        onMounted(() => {
            console.log(attrs);
            console.log(slots);
        });

        const submit = () => {
            emit("submit", "ini adalah emit dari user component")
        }

        return { description };
    }
}
</script>