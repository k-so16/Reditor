<template>
  <q-layout view="lHh Lpr lFf">
    <q-bar class="q-electron-drag bg-black text-white">
      <div class="cursor-pointer q-electron-drag--exception">
        File
        <q-menu>
          <q-list dense>
            <q-item clickable v-close-popup @click="save">
              <q-item-section>Save</q-item-section>
            </q-item>
            <q-item clickable v-close-popup @click="close">
              <q-item-section>Quit</q-item-section>
            </q-item>
          </q-list>
        </q-menu>
      </div>
      <q-space />
      <q-btn dense flat icon="minimize" @click="minimize" />
      <q-btn dense flat icon="crop_square" @click="maximize" />
      <q-btn dense flat icon="close" @click="close" />
    </q-bar>
    <q-page-container>
      <router-view :file.sync="file" />
    </q-page-container>
  </q-layout>
</template>

<script>
import { openURL } from 'quasar';
import { remote } from 'electron';
import fs from 'fs';

export default {
  name: 'MyLayout',
  data() {
    return {
      file: {
        path: null,
        content: null,
      },
    };
  },
  methods: {
    openURL,
    minimize() {
      remote.BrowserWindow.getFocusedWindow().minimize();
    },
    maximize() {
      const win = remote.BrowserWindow.getFocusedWindow();
      if (win.isMaximized()) {
        win.unmaximize();
      } else {
        win.maximize();
      }
    },
    close() {
      remote.BrowserWindow.getFocusedWindow().close();
    },
    save() {
      if (!this.file.path) {
        const filePath = remote.dialog.showSaveDialog(
          remote.BrowserWindow.getFocusedWindow(),
          {
            defaultPath: process.cwd(),
          },
        );
        if (!filePath) return;
        this.file.path = filePath;
      }
      fs.writeFile(this.file.path, this.file.content, { encoding: 'utf-8' }, (err) => {
        if (err) throw err;
      });
    },
  },
};
</script>

<style>
</style>
