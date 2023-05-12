<template>
    <div class="home-view">
    <!--Setting title and upload button to true for this view-->
    <NavBar :title="title" :showupload="showUpload" />
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

  data() {
    return {
      title: 'Photo Album',
      showUpload: true,
    }
  }
}
</script>

<style scoped>
.home-view {
  background-color: #edf6f9;
  height: 100%;
  
}
</style>