<template>
  <div class="welcome-view">
    <LogIn />
  </div>
</template>

<script>
import { defineComponent } from 'vue';

// Components
import TitleHeader from '../components/WelcomeView/TitleHeader.vue';
import LogIn from '../components/WelcomeView/LogIn.vue';

export default defineComponent({
  name: 'WelcomeView',

  components: {
    TitleHeader,
    LogIn,
  },
});
</script>

<style scoped>
.welcome-view {
  background-color: #a0c4ff; /* Update the background color to red */
  height: 100vh;
  
}



</style>