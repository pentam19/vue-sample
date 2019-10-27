<template>
    <div>
        <h3>User</h3>
        <p>{{ count }}</p>
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
    computed: {
        count() {
            return this.$store.state.count;
        }
    }
};
</script>
