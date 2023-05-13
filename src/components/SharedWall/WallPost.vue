<template>
  <v-row>
    <v-col>
      <ul class="image-list">
        <li
          v-for="(image, index) in images"
          :key="index"
        >
          <v-card class="outtercard">
            <v-card class="innercard">
              <v-img :src="image.url" :alt="image.alt" aspect-ratio="1" cover>
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
            <h3>{{ image.description }}</h3>
            <v-icon @click="toggleCommentSection(index)" color="#83c5be" large>mdi-message</v-icon>
            <div class="comment-section" v-if="image.showComments">
              <form @submit.prevent="submitComment(index, comment)">
                <v-textarea
                  v-model="comment"
                  placeholder="Add a comment..."
                  rows="3"
                  hide-details
                ></v-textarea>
                <v-btn type="submit" color="#83c5be">Post Comment</v-btn>
              </form>
              <div v-for="(comment, cIndex) in image.comments" :key="cIndex">
                <p>{{ comment }}</p>
              </div>
            </div>
          </v-card>
        </li>
      </ul>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: 'WallPost',
  components: {
  },
  data() {
    return {
      comment: '',
      images: [
        { url: 'https://www.nzherald.co.nz/resizer/nMnOW002P5OId4ALq6KPS1P-H6M=/576x400/smart/filters:quality(70)/cloudfront-ap-southeast-2.images.arcpublishing.com/nzme/VGUXHQH4NUBOEAO3QB35PECED4.jpg', alt: 'Image 1', description: 'Crazy Night', comments: [], showComments: false },
        { url: 'https://bilder.bild.de/fotos-skaliert/diddy-und-sein-smartphone--frueher-waren-sie-unzertrennlich-200732755-55154094/1,w=1192,q=low,c=0.bild.jpg', alt: 'Image 2', description: 'Fur like a Bear', comments: [], showComments: false },
        { url: 'https://d.newsweek.com/en/full/1809454/puff-daddy-jennifer-lopez.jpg', alt: 'Image 3', description: 'Me and J. Lo', comments: [], showComments: false }
      ],
    };
  },
  methods: {
    toggleCommentSection(imageIndex) {
      this.images[imageIndex].showComments = !this.images[imageIndex].showComments;
    },
    submitComment(imageIndex, comment) {
      if (comment.trim() !== '') {
        this.images[imageIndex].comments.push(comment);
        this.comment = '';
      }
    },
  },
}
</script>

<style scoped>
.outtercard {
  background-color: rgb(255, 255, 255);
  width: 20%; 
  margin: auto;
  border: 3px solid black;
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
  max-width: 100%; 
}

h3 {
  font-family: "Shadows Into Light Two", cursive;
  font-size: 30px;
  line-height: 10px;
  text-align: center;
  margin-bottom: 10%;
}

.image-list {
  list-style-type: none;
  padding: 0;
}

.image-list li {
  text-align: center;
  margin-bottom: 30px;
}

.v-btn {
  background-color: #83c5be;
    color: #000000;
    font-size: 15px;
    font-weight: bold;
    text-transform: capitalize;
    text-align: center;
    margin: 15px;
}

.v-col {
  margin-top: 3vh;
}
</style>
