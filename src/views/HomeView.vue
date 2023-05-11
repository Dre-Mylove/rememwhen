<template>
    <div class="home-view">
    <NavBar />
    <Image />
    </div>
</template>

<script>
import Image from '@/components/HomeView/Image.vue';
import NavBar from '@/components/HomeView/NavBar.vue';

export default {
  name: 'HomeView',
  components: {
    Image,
    NavBar,
  },
}

</script>

<style scoped>
.home-view {
  background-color: #a0c4ff;
  height: 100%;
  
}
</style>