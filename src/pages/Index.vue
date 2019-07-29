<template>
  <q-page class="flex flex-center">
    <img alt="Quasar logo" src="~assets/quasar-logo-full.svg">
  </q-page>
</template>

<style>
</style>

<script>
import fs from 'fs';

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
  methods: {
    loadItems() {
      fs.readdir(this.currentDir, (err, files) => {
        if (err) throw err;
        this.list = files.map((file) => {
          const isFile = fs.statSync(file).isFile();
          return {
            name: file,
            isFile,
          };
        });
      });
    },
  },
  mounted() {
    this.loadItems();
  },
};
</script>
