<template>
  <v-main>
    <v-main>
    <app-bar></app-bar>
    <v-spacer></v-spacer>
      <v-fade-transition mode='out-in'>
        <router-view></router-view>
      </v-fade-transition>
    </v-main>
  </v-main>
</template>

<script>
import AppBar from '@/components/core/AppBar.vue';

export default {
  name: 'AppContainer',
  components: {
    AppBar,
  },
};
</script>
