<template>
    <v-main>
      <v-container>
        <v-row>
          <v-col cols="12" sm="6" md="4" v-for="(friend, index) in friends" :key="index">
            <v-card class="outter mx-auto my-3" elevation="5">
              <v-card-title>
                <v-avatar size="64" class="mr-3">
                  <v-img :src="friend.avatar" :alt="friend.name" class="avatar-img" />
                </v-avatar>
                {{ friend.name }}
              </v-card-title>
              <v-card-text>
                <v-select
                  :items="friend.communities"
                  label="Communities"
                  outlined
                ></v-select>
              </v-card-text>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </template>
  
  <script>
  export default {
    name: "Friends",
    data() {
      return {
        friends: [
          {
            name: "Esteicy Rangel",
            email: "Ido@Gmail.com",
            communities: ["Immediate Family", "Family"],
            avatar: "https://randompicturegenerator.com/img/people-generator/g1f3229025c3d5bfe285df1d4bad25c71ec473af8e98d80bb634561616ccd9788e5486c896768a6c1b04aeafa2fae4746_640.jpg",
          },
          {
            name: "Jane Smith",
            email: "jane@example.com",
            communities: ["Tesla", "Church"],
            avatar: "https://randompicturegenerator.com/img/people-generator/g69b41a50682984f0e04b9720b4dc30d30e91cabaa59cdc4edf0dd41918f85cd798335f5b3d69811ad9b191d51839a79c_640.jpg",
          },
          {
            name: "Buddy Love",
            email: "sam@example.com",
            communities: ["Tesla", "Barbershop"],
            avatar: "https://cdn.pixabay.com/photo/2018/01/24/19/49/people-3104635_640.jpg",
          },
          {
            name: "Sara White",
            email: "sara@example.com",
            communities: ["Kids Daycare", "Church"],
            avatar: "https://cdn.pixabay.com/photo/2016/11/08/05/10/students-1807505_960_720.jpg",
          },
        ],
      };
    },
  };
  </script>

  <style scoped>

.v-card:hover {
    box-shadow: 0 24px 24px rgba(0, 0, 0, 0.1), 0 24px 24px rgba(0, 0, 0, 0.1),
    0 24px 24px rgba(0, 0, 0, 0.1);
}


.title {
    color: #000000;
    font-size: 40px;
    font-weight: bold;
    
    margin: 6%;
}

.v-select {
    color: #000000;
    
 
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


    </style>