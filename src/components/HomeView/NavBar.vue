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
    <v-toolbar>
      <v-btn icon @click="closeDialog">
        <v-icon>mdi-close</v-icon>
      </v-btn>
      <v-toolbar-title class="dialog-title" >
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
    const drawer = ref(false);

    return {
      isActive,
      dialog,
      drawer,
    };
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
