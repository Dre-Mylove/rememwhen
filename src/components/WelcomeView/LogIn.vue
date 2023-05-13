<template>
     <h1>RemembrWhen </h1>
    <v-card class="outterpart">
      <v-card class="image mx-auto px-6 py-8" max-width="344">
        <v-form
          v-model="form"
          @submit.prevent="onSubmit"
        >
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
            :readonly="loading"
            :rules="[required]"
            clearable
            label="Password"
            placeholder="Enter your password"
          ></v-text-field>

          
       
  
          <br>
  
          <v-btn
            
            :loading="loading"
            block
            size="large"
            type="submit"
            variant="elevated"
            :to="'/Home'"
          >
            Sign In
          </v-btn>
        </v-form>
      </v-card>
      <div class="signup">
        Don't have an account? <a href="#" @click.prevent="$emit('toggleSignUp')">Sign Up</a>
      </div>    </v-card>
  </template>

<script>

export default {
  name: 'LogIn',
}
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

.v-btn {
  background-color: #83c5be;
  color: black;
  /* font-family: Arial, Helvetica, sans-serif; */
  font-size: 20px;
  font-weight: bold;
}

a {
    color: #83c5be;
    text-decoration: none;}

.outterpart {
    background-color:rgb(255, 255, 255);
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