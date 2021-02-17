<template>
  <div class="bg-yellow-300">
    <div class="p-14">
      <router-link class="flex justify-center text-4xl text-blue-700" to="/">
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
