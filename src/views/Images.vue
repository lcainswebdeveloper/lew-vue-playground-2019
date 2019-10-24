<template>
  <div class="home">
    <h3 class="text-center mb-10">
      Choose From The Menu Below
    </h3>
    <image-with-loader :img-src="slide1" img-width="1920" img-height="1200"></image-with-loader>
  </div>
</template>

<script>
// @ is an alias to /src
const slide1 = require('@/assets/img/slide1.jpg');

export default {
  components: {
    ImageWithLoader: () => import('@/components/Images/WithLoader'),
  },
  name: 'Images',
  data() {
    return {
      slide1,
    };
  },
};
</script>
