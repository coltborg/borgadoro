<template>
  <div class="title-bar"></div>
</template>

<script>
export default {
  name: 'TitleBar',
};
</script>

<style scoped>
.title-bar {
  -webkit-app-region: drag;
  -webkit-user-select: none;
  user-select: none;
  height: var(--title-bar-height);
  width: 100%;
}
</style>
