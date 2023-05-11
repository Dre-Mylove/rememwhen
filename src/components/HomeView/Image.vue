<template>
  <v-row>
    <v-col v-for="n in 9" :key="n" cols="4">
      <v-card class="outtercard">
        <v-card class="innercard">
          <v-img
            :src="`https://picsum.photos/500/300?image=${n * 5 + 10}`"
            :lazy-src="`https://picsum.photos/10/6?image=${n * 5 + 10}`"
            aspect-ratio="1"
            cover
          >
            <template v-slot:placeholder>
              <v-row align="center" justify="center">
                <v-progress-circular
                  indeterminate
                  color="grey-lighten-5"
                ></v-progress-circular>
              </v-row>
            </template>
          </v-img>
        </v-card>
        <h3>computer science</h3>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: "Image",
};
</script>

<style scoped>
.outtercard {
  background-color: rgb(255, 255, 255);
  width: 70%;
  margin: auto;
  border: 5px solid black;
  height: 100%;
}

.innercard {
  margin: 5%;
  margin-bottom: 10%;
  background-color: black;
  height: 75%;
}

.v-img {
  border: 2px solid black;
}

h3 {
  font-family: "Shadows Into Light Two", cursive;
  font-size: 30px;

  line-height: 5px;
  text-align: center;
}
</style>
