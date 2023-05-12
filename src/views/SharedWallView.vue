<template>
  <div class="shared-wall-view">
    <NavBar :title="title" :showupload="showUpload"/>
    <WallPost />
  </div>
</template>

<script>
import NavBar from "@/components/HomeView/NavBar.vue";
import WallPost from "@/components/SharedWall/WallPost.vue";

export default {
  name: "SharedWallView",

  components: {
    NavBar,
    WallPost,
  },  

  data() {
    return {
      title: "Shared Wall",
      showUpload: false,
    };
  },
};

</script>

<style scoped>
.shared-wall-view {
  background-color: #edf6f9;
  height: 100%;
}

</style>