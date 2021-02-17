<template>
  <div>
    <div class="p-14">
      <router-link class="flex justify-center text-4xl text-yellow-700" to="/">
      Pokemon Search
      </router-link>
    </div>
    <router-view />
  </div>
</template>

<script>
export default {
  name: "App"
};
</script>
<style>
</style>
