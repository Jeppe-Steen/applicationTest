<template lang="pug">
  nav
    nuxt-link(to="/") Home
    nuxt-link(to="/icon") Icon animation
    nuxt-link(to="/comment") Comment the code
    nuxt-link(to="/component") Component creation
</template>

<script>
export default {
  name: 'NavigationComponent',
}
</script>

<style scoped>
nav {
  display: flex;
  justify-content: flex-start;
  padding: 21px 20px;
  flex-direction: row;
  background: #ffffff;
  box-shadow: 0 1px 5px 1px rgba(0, 0, 0, 0.4);
}

nav a {
  margin-right: 12px;
  text-decoration: none;
  letter-spacing: 1.4px;
  border: 1px solid #263232;
  border-radius: 4px;
  padding: 8px 12px;
  color: #343744;
}
</style>
