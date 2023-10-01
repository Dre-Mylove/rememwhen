<template>
    <div>
    <h1>Friend Venn</h1>
    <v-card class="outterpart">
      <v-card class="image mx-auto px-6 py-8" max-width="344">
        <v-form v-model="form" @submit.prevent="onSubmit">
          
            <v-text-field
              v-model="firstname"
              :readonly="loading"
              :rules="[required]"
              class="mb-2"
              clearable
              label="First Name"
            ></v-text-field>
  
            <v-text-field
              v-model="lastname"
              :readonly="loading"
              :rules="[required]"
              class="mb-2"
              clearable
              label="Last Name"
            ></v-text-field>
         
          <v-text-field
            v-model="email"
            :readonly="loading"
            :rules="[required]"
            class="mb-2"
            clearable
            label="Email"
          ></v-text-field>
  
          <v-text-field
            v-model="password"
            :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
            :rules="[rules.required, rules.min]"
            :type="show1 ? 'text' : 'password'"
            name="input-10-1"
            label="Password"
            hint="At least 8 characters"
            counter
            @click:append="show1 = !show1"
          ></v-text-field>
          <br />
  
          <v-btn
            :loading="loading"
            block
            size="large"
            type="submit"
            color="#83c5be"
            outlined
            :to="'/Home'"
            @click="onSubmit"
          >
            Submit
          </v-btn>
        </v-form>
      </v-card>
      <div class="signin">
  Already have an account? <a href="#" @click.prevent="$emit('toggleSignUp')">Sign In</a>
</div>
    </v-card>
    </div>
  </template>
  
  <script>
  import { getAuth, createUserWithEmailAndPassword } from 'firebase/auth';
  import { app } from '@/firebase/firebase'

  export default {
    name: "SignUp",
    data() {
      return {
        form: true,
        firstname: "",
        lastname: "",
        email: "",
        password: "",
        show1: false,
        loading: false,
        required: (value) => !!value || "Required.",
        rules: {
          required: (value) => !!value || "Required.",
          min: (value) => value.length >= 8 || "Min 8 characters",
        },
      };
    },
    methods: {
      onSubmit() {
        const auth = getAuth(app);
        createUserWithEmailAndPassword(auth, this.email, this.password)
          .then((userCredential ) => {
            const user = userCredential.user;
          })
          .catch((error) => {
            const errorCode = error.code;
            const errorMessage = error.message;
          })
      },
    },
  };
  </script>

<style scoped>
.image {
  margin-top: 5%;
  background-color: black;
}

div {
  text-align: center;
  font-size: 20px;
  font-weight: bold;
  color: black;

  margin-bottom: 5%;
}

a {
  color: #83c5be;
}

.v-btn {
  background-color: #83c5be;
  color: black;
  /* font-family: Arial, Helvetica, sans-serif; */
  font-size: 20px;
  font-weight: bold;
}

.outterpart {
  background-color: rgb(255, 255, 255);
  width: 25%;
  margin: auto;
  border: 5px solid black;
  height: 60%;
}

.v-text-field {
  background-color: white;
}

h1 {
  text-align: center;
  font-size: 45px;
  font-weight: bold;
  color: black;
  font-family: cursive;
  margin-bottom: 5%;
}
</style>
