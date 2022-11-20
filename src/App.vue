<template>
  <div id="app">
    <appHeader />
    <appMain />
  </div>
</template>

<script>
  import 'axios';

  import appHeader from './components/appHeader.vue';
  import appMain from './components/appMain.vue';
  export default {
    name: 'App',
    components: {
      appHeader,
      appMain,
    }
  }

</script>

<style lang="scss"></style>
