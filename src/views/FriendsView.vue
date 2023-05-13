<template>
    <div class="friends-view">
        <NavBar :title="title" />
        <Friends :friends="friends" />
    </div>

</template>

<script>
import Friends from '@/components/Friends/Friends.vue';
import NavBar from '@/components/HomeView/NavBar.vue';

export default {
  name: 'FriendsView',

    components: {
        Friends,
        NavBar,
    },

    data() {

        return {title: 'Friends',}
    }
}
</script>

<style scoped>

.friends-view {
    background-color: #edf6f9; /* Update the background color to red */
    height: 100vh;
    
}
</style>