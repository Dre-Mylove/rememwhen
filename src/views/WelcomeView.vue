<template>
  <div class="welcome-view">
    <LogIn v-if="!showSignUp" @toggleSignUp="toggleSignUp" />
    <SignUp v-else @toggleSignUp="toggleSignUp" />
  </div>
</template>

<script>
import { defineComponent } from 'vue';

// Components
import TitleHeader from '../components/WelcomeView/TitleHeader.vue';
import LogIn from '../components/WelcomeView/LogIn.vue';
import SignUp from '../components/WelcomeView/SignUp.vue';

export default defineComponent({
  name: 'WelcomeView',

  components: {
    TitleHeader,
    LogIn,
    SignUp,
  },

  data() {
    return {
      showSignUp: false,
    };
  },

  methods: {
    toggleSignUp() {
      this.showSignUp = !this.showSignUp;
    },
  },
});
</script>

<style scoped>
.welcome-view {
  background-color: #edf6f9; /* Update the background color to red */
  height: 100vh;
  
}



</style>