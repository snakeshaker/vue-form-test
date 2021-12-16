<template>
  <div class="container" v-cloak>
    <form-main/>
  </div>
</template>

<script>
import FormMain from './components/FormMain.vue'

export default {
  name: 'App',
  components: {
    FormMain,
  },
}
</script>

<style>
@import './assets/css/styles.css';
</style>
