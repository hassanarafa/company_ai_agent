<template>
  <div id="app" class="bg-slate-950 min-h-screen text-slate-100" dir="rtl">
    <HelloWorld />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  }
}
</script>

<style>
body {
  margin: 0;
  background-color: #000000;
}
</style>