<template>
  <v-app-bar density="compact">
    <template v-slot:prepend>
      <v-app-bar-nav-icon></v-app-bar-nav-icon>
    </template>

    <v-app-bar-title>Photo Album</v-app-bar-title>

    <v-btn class="uploadbtn" @click="showDialog">Upload</v-btn>
  </v-app-bar>

  <!--Dialog pop up to upload pictures-->

  <v-dialog  transition="dialog-top-transition"  v-model="dialog">
    <v-card>
    <v-toolbar>
      <v-btn icon @click="closeDialog">
        <v-icon>mdi-close</v-icon>
      </v-btn>
      <v-toolbar-title class="dialog-title">
        Upload Photo
      </v-toolbar-title>
    </v-toolbar>
    <v-card class="in-development">
      <v-img src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/49/A_black_image.jpg/640px-A_black_image.jpg"></v-img>
    </v-card>
    </v-card>
  </v-dialog>
</template>

<script>
import { ref } from "vue";

export default {
  name: "NavBar",

  setup() {
    const isActive = ref(false);
    const dialog = ref(false);

    return {
      isActive,
      dialog,
    };
  },

  methods: {
    toggle() {
      this.isActive = !this.isActive;
    },

    showDialog() {
      this.dialog = true;
    },

    closeDialog() {
      this.dialog = false;
    },
  },
};
</script>

<style scoped>
.v-app-bar {
    background-color: #a0c4ff;
}

.v-app-bar-title {
    color: #000000;
    font-size: 40px;
    font-weight: bold;
    text-align: center;
}

.uploadbtn {
    background-color: #ffd6a5;
    color: #000000;
    font-size: 15px;
    font-weight: bold;
    text-align: center;
}

.in-development {
    background-color: #ffd6a5;
    color: #000000;
    font-size: 15px;
    font-weight: bold;
    text-align: center;
    height: 10%;
    margin: 10%;
}

.v-dialog { 
    color: #000000;
    font-size: 15px;
    font-weight: bold;
    text-align: center;
    height: 100%;
    width: 30%;
}

.dialog-title {
    color: #000000;
    font-size: 20px;
    font-weight: bold;
    text-align: center;
    margin-left: -10%;
}
</style>
