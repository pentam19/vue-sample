<template>
  <div>
    <h1>{{ msg2 }}</h1>
    <button @click="addWorld">addWorld</button>
  </div>
</template>

<script>
export default {
  name: 'Test',
  props: {
    msg2: String
  },
  methods: {
      addWorld() {
          this.$emit("add-world", this.msg2 + ' World');
      }
  }
}
</script>
