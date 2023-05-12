<template>
  <v-app-bar >
    <v-app-bar-nav-icon @click="drawer = true" class="d-flex d-sm-none"></v-app-bar-nav-icon>
    <v-toolbar-title class="title">{{ title }}</v-toolbar-title>
    <v-spacer></v-spacer>
    <v-btn class="navbtns" v-if="!showupload" :to="'/home'"> Home</v-btn>
    <v-btn class="navbtns" v-if="showupload"  @click="showDialog">Upload</v-btn>
    <v-btn class="navbtns">New Wall</v-btn>
    <v-btn class="navbtns">Friends</v-btn>
    
    <v-btn class="navbtns" :to="'/'">Logout</v-btn>
  </v-app-bar>

  <v-navigation-drawer v-model="drawer" app>
    <v-list>
      <v-list-item v-for="item in items" :key="item.title" link>
        <v-list-item-icon>
          <v-icon>{{ item.icon }}</v-icon>
        </v-list-item-icon>
        <v-list-item-content>
          <v-list-item-title>{{ item.title }}</v-list-item-title>
        </v-list-item-content>
      </v-list-item>
    </v-list>
  </v-navigation-drawer>

  <!--Dialog pop up to upload pictures-->

  <v-dialog  transition="dialog-top-transition"  v-model="dialog">
    <v-card>
    <v-toolbar class="dialogbar">
      <v-btn icon @click="closeDialog">
        <v-icon>mdi-close</v-icon>
      </v-btn>
      <v-toolbar-title class="dialog-title" >
        Upload Photo
      </v-toolbar-title>
    </v-toolbar>
    <v-card class="in-development">
      <v-img :src="noteImage" contain v-if="noteImage"></v-img>
    </v-card>
    <v-file-input
        label="File input"
        accept="image/*"
        variant="solo-filled"
        
        @change="previewImage"
      ></v-file-input>
    <v-text-field
      class="input"
      dense
      outlined
      label="Caption"
      maxLength="20"
      prepend-icon="mdi-message"
      >
      </v-text-field>
      <v-btn class="submitbtn" @click="closeDialog">Submit</v-btn>
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
    const drawer = ref(false);
    const noteImage =ref("https://static.vecteezy.com/system/resources/thumbnails/016/776/618/small_2x/an-old-polaroid-camera-in-color-and-in-black-and-white-the-concept-of-the-old-polaroid-technique-free-vector.jpg");

    return {
      isActive,
      dialog,
      drawer,
      noteImage,
    };
  },

  data() {
    return {
      file: null,
    }
  },

    props: {
      title: {
        type: String,
      },
      showupload: {
        type: Boolean,
        
      },
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

    previewImage(e) {
      const file = e.target.files[0];
      this.file = file;
      const reader = new FileReader();
      reader.readAsDataURL(file);
      reader.onload = (e) => {
        this.noteImage = e.target.result;
      };
    },
  },
};
</script>

<style scoped>
.v-app-bar {
    background-color: #edf6f9;
}

.title {
    color: #000000;
    font-size: 40px;
    font-weight: bold;
    
    margin: 6%;
}

.navbtns {
    background-color: #83c5be;
    color: #000000;
    font-size: 15px;
    font-weight: bold;
    text-align: center;
    margin: 15px;
}
.v-app-bar-title {
    color: #000000;
    font-size: 40px;
    font-weight: bold;
    margin: auto;
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
    width: 40%;
}

.dialogbar {
    background-color: #edf6f9;
    color: #000000;
    font-size: 15px;
    font-weight: bold;
    text-align: center;
    height: 10%;
    width: 100%;
    margin: 0%;
}

.dialog-title {
    color: #000000;
    font-size: 20px;
    font-weight: bold;
    text-align: center;
    margin-left: -10%;
}

.v-text-field {
    color: #000000;
    font-size: 15px;
    font-family: "Shadows Into Light Two", cursive;
    font-weight: bold;
    text-align: center;
    height: 10%;
    width: 75%;
    margin-inline: 10%;
}

.submitbtn {
  background-color: #83c5be;
    color: #000000;
    font-size: 15px;
    font-weight: bold;
    text-align: center;
    margin: 15px;
    margin-inline: 40%;
    margin-bottom: 5%;
}

.v-file-input {
  color: #000000;
    font-size: 15px;
    font-family: "Shadows Into Light Two", cursive;
    font-weight: bold;
    text-align: center;
    height: 10%;
    width: 75%;
    margin-inline: 10%;
}
</style>
