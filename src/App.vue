
<template>
  <app-layout>
    <Home />
  </app-layout>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

import AppLayout from './layout/AppLayout.vue';
import Home from './pages/Home.vue';

export default defineComponent({
  components: {
    AppLayout,
    Home
  }
})
</script>