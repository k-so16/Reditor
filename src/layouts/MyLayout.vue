<template>
  <q-layout view="lHh Lpr lFf">
    <q-bar class="q-electron-drag">
      <div class="cursor-pointer q-electron-drag--exception">
        File
        <q-menu>
          <q-list dense>
            <q-item clickable>
              <q-item-section>Save</q-item-section>
            </q-item>
            <q-item clickable>
              <q-item-section>Quit</q-item-section>
            </q-item>
          </q-list>
        </q-menu>
      </div>
      <q-space />
      <q-btn dense flat icon="minimize" />
      <q-btn dense flat icon="crop_square" />
      <q-btn dense flat icon="close" />
    </q-bar>
    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { openURL } from 'quasar';

export default {
  name: 'MyLayout',
  data() {
    return {
    };
  },
  methods: {
    openURL,
  },
};
</script>

<style>
</style>
