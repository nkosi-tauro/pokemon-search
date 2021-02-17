<template>
  <div>
    <particles-bg type="fountain" :bg="true" />
    <div class="p-14">
      <router-link class="flex justify-center text-4xl text-yellow-700" to="/">
      Pokemon Search
      </router-link>
    </div>
    <router-view />
  </div>
</template>

<script>
import { ParticlesBg } from "particles-bg-vue";
export default {
  name: "App",
  components: {
    ParticlesBg,
  }
};
</script>
<style>
</style>
