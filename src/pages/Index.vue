<template>
  <q-page class="flex flex-center">
    <img alt="Quasar logo" src="~assets/quasar-logo-full.svg">
  </q-page>
</template>

<style>
</style>

<script>
export default {
  name: 'PageIndex',
  data() {
    return {
      currentDir: process.cwd(),
      currentFile: null,
      filterPattern: '',
      list: [],
      editor: null,
    };
  },
};
</script>
