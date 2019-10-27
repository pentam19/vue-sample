<template>
    <div>
        <h3>Home</h3>
        <button @click="increment">+1</button>
        <button @click="decrement">-1</button>
        <p>{{ test }}</p>
    </div>
</template>

<script>
export default {
    data() {
        return {
            test: "Test"
        }
    },
    methods: {
        increment() {
            this.$store.state.count++;
        },
        decrement() {
            this.$store.state.count--;
        }
    }
};
</script>
