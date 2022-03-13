<template>
  <h1 class="text-3xl font-bold underline">Hello world!</h1>
  <svg-icon :fa-icon="faGithub" :size="50"></svg-icon>
</template>

<script>
import { faGithub } from "@fortawesome/free-brands-svg-icons";
export default {
  setup() {
    return {
      faGithub,
    };
  },
};
</script>

<style>
</style>
