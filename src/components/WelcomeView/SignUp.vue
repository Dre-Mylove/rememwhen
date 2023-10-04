<template>
  <div>
    <h1>Friend Venn</h1>
    <v-card class="outterpart">
      <v-card class="image mx-auto px-6 py-8" max-width="344">
        <v-form v-model="form" @submit.prevent="onSubmit">
          <!-- User Registration Form -->
          
          <!-- First Name Field (Commented out) -->
          <!--
          <v-text-field
            v-model="firstname"
            :readonly="loading"
            :rules="[required]"
            class="mb-2"
            clearable
            label="First Name"
          ></v-text-field>
          -->

          <!-- User Name Field -->
          <v-text-field
            v-model="username"
            :rules="[rules.required, usernameValidator, rules.usernameMax]"
            class="mb-2"
            clearable
            counter
            label="User Name"
            @input="filterUsername" 
            @keyup="debouncedCheckUsername" 
            @focus="isFocused = true"
            @blur="isFocused = false"
          >
            <!-- Checkmark (✔) displayed when conditions met -->
            <span v-if="usernameAvailable && username.length >= 3 && username.length <= 15" class="checkmark">&#10004;</span>
            <!-- 'X' (✖) displayed when username is unavailable and length condition met -->
            <span v-if="!usernameAvailable && username.length >= 3" class="x">&#10006;</span>
            <!-- '@' displayed when the field is focused -->
            <span v-if="isFocused | username.length != 0">@</span>
          </v-text-field>

          <!-- Last Name Field (Commented out) -->
          <!--
          <v-text-field
            v-model="lastname"
            :readonly="loading"
            :rules="[required]"
            class="mb-2"
            clearable
            label="Last Name"
          ></v-text-field>
          -->

          <!-- Email Field -->
          <v-text-field
            v-model="email"
            :readonly="loading"
            :rules="[rules.required]"
            class="mb-2"
            clearable
            label="Email"
          ></v-text-field>

          <!-- Password Field -->
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

          <!-- Submit Button -->
          <v-btn
            :loading="loading"
            :disabled="!usernameAvailable"
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
      <!-- Sign In Link -->
      <div class="signin">
        Already have an account?
        <a href="#" @click.prevent="$emit('toggleSignUp')">Sign In</a>
      </div>
    </v-card>
  </div>
</template>

<script>
import { getAuth, createUserWithEmailAndPassword } from "firebase/auth";
import { app, db } from "@/firebase/firebase";
import { setDoc, doc, getDoc } from "firebase/firestore";
import debounce from "lodash/debounce";

export default {
  name: "SignUp",
  data() {
    return {
      // Data properties for the form
      form: true,
      firstname: "",
      lastname: "",
      username: "",
      email: "",
      password: "",
      show1: false,
      loading: false,
      usernameAvailable: false,
      isFocused: false,
      rules: {
        required: (value) => !!value || "Required.",
        usernameMax: (value) => value.length <= 15 || "Max 15 characters",
        min: (value) => value.length >= 8 || "Min 8 characters",        
      },
      // Validator for username to allow only specific characters
      usernameValidator: (value) => {
        const regex = /^[a-zA-Z0-9_]+$/;
        if (!regex.test(value)) {
          return 'Only letters, numbers, and underscores are allowed.';
        }
        return true;
      },
    };
  },
  methods: {
    // Method to debounce the username checking
    debouncedCheckUsername() {
      // Wrap the debounce function in a Promise
      return new Promise((resolve) => {
        debounce(async () => {
          await this.checkUsername();
          console.log("Debounced function called");
          resolve();
        }, 100)();
      });
    },
    // Method to check if the username is available
    async checkUsername() {
      try {
        // Check if the username already exists
        const username = this.username;

        if (username.length >= 1 && username.length <= 15) {
          const usernameRef = doc(db, "username", username.toLowerCase());
          const docSnapshot = await getDoc(usernameRef);

          this.usernameAvailable = !docSnapshot.exists();
          console.log("Username available:", this.usernameAvailable);
        } else {
          // Handle invalid username length if needed
          this.usernameAvailable = false;
          console.log("Username available:", this.usernameAvailable);
        }
      } catch (error) {
        // Handle any errors that occur during the database query
        console.error("Error checking username:", error);
        this.usernameAvailable = false; // Set to false in case of an error
      }
    },
    // Method to filter username input to allow only specific characters
    filterUsername() {
      // Remove characters that are not allowed
      this.username = this.username.replace(/[^a-zA-Z0-9_]/g, '');
    },
    // Method to handle form submission
    async onSubmit() {
      this.loading = true;
      const auth = getAuth(app);

      try {
        const userCredential = await createUserWithEmailAndPassword(
          auth,
          this.email.toLowerCase(),
          this.password
        );

        // Save the user document
        const userRef = doc(db, "users", userCredential.user.uid);
        await setDoc(userRef, {
          username: this.username.toLowerCase(),
          email: this.email.toLowerCase(),
        });

        // Save the username document
        const usernameRef = doc(db, "usernames", this.username);
        await setDoc(usernameRef, {
          email: this.email,
          uid: userCredential.user.uid,
        });

        this.loading = false;
      } catch (error) {
        console.error("Error creating user:", error);
        this.loading = false;
      }
    },
  },
};
</script>

<style scoped>
.image {
  margin-top: 5%;
  background-color: black;
}

.checkmark {
  position: absolute;
  top: 50%;
  right: 12px;
  color: green;
}

.x {
  position: absolute;
  top: 50%;
  right: 12px;
  color: red;
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

@media screen and (max-width: 600px) {
  .outterpart {
    width: 100%;
  }
}
</style>
