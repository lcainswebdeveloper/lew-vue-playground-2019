<template>
  <div id="app">
    <div id="nav" class="bg-grey-lighter p-2 text-center">
      <router-link to="/">Home</router-link> |
      <router-link to="/dropdown">Custom Dropdown</router-link>
    </div>
    <div class="router-view mx-auto px-8 mt-8">
      <router-view/>
    </div>
  </div>
</template>

<script>
require('normalize.css/normalize.css');
</script>
<style src="./assets/sass/tailwind.css">
