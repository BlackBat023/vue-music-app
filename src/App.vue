<template>
  <Header />
  <router-view/>
</template>

<script>
import Header from '@/components/Header.vue'
import HomeView from '@/views/HomeView.vue'

export default {
  name: 'App',
  components: {
    Header,
    HomeView
  },
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
}

</style>
