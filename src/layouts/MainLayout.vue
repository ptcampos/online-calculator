<template>
  <q-layout view="lHh Lpr lFf">
    <q-page-container>
      <router-view />
    </q-page-container>
    <div class="text-center text-white fixed-bottom q-mb-md">
      Powered by
      <a class="link" target="__blank" href="https://quasar.dev/">Quasar</a>
      and Made with <q-icon color="pink" name="ion-heart" /> by
      <a class="link" target="__blank" href="https://github.com/ptcampos">Paulo Campos</a>
    </div>
  </q-layout>
</template>

<script>
export default {
  name: 'MainLayout',

  data() {
    return {
      leftDrawerOpen: false,
      essentialLinks: []
    }
  }
}
</script>

<style lang="scss">
.link {
  color: white;
  text-decoration: none;
}
</style>
