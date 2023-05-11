<template>
     <h1>Remember When </h1>
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
          >
            Sign In
          </v-btn>
        </v-form>
      </v-card>
     
    </v-card>
  </template>

<script>

export default {
  name: 'LogIn',
}
</script>

<style scoped>
.image {
    margin-top: 10%;
    background-color: black;
    
}

.v-btn {
  background-color: #a0c4ff;
  color: black;
}

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