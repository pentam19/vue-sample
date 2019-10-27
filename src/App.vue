<template>
  <div>
    <nav>
      <router-link to="/" class="link">Home</router-link>
      <router-link to="/users" class="link">Users</router-link>
      <router-link to="/sofmap" class="link">Sofmap</router-link>
    </nav>
    <router-view></router-view>
  </div>
</template>

<style scoped>
.link {
  margin-right: 10px;
}
</style>
