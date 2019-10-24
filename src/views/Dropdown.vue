<template>
  <div class="home">
    <h3 class="text-center">
      Custom Dropdown
    </h3>
    <h5 class="mt-4 text-center">Choose an option</h5>
    <custom-dropdown></custom-dropdown>
  </div>
</template>

<script>
// @ is an alias to /src
export default {
  components: {
    CustomDropdown: () => import('@/components/Dropdowns/Custom'),
  },
  name: 'dropdown',
};
</script>
