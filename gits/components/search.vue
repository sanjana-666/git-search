<script setup>
// import {ref} from  vue

const username = ref('');
const userProfile = ref(null);
const error = ref(null);

const  getUserProfile = async ()=>{
    try{
   
        const response = await fetch(`https://api.github.com/users/${username.value}`)
        const data = await response.json()

        if(response.ok)
    {
        userProfile.value = data;
        error.value = null;
    }
    else{
       userProfile.value = null
       error.value = `Error: ${data.message}`

    }

    }
    catch(err)
    {
        console.error("Error fetching data",err)
        error.value = 'An error occured while fetching data'
    }
}
</script>

<template>
  
    <div class="github-profile">
        <h1 class="app-title">
            Github User Profile
        </h1>

        <div class="input-container">
            <input v-model="username" placeholder="Enter github username" @input="getUserProfile">
        </div>
    </div>
    <div v-if="userProfile" class=" user-profile">
        <img :src="userProfile.avatar_url" :alt="userProfile.login">

    
        <div class="user-details">
            <p><strong>Name: </strong>{{userProfile.login}}</p>
            <p><strong>Location: </strong>{{userProfile.location}}</p>
            <p><strong>Followers: </strong>{{userProfile.followers}}</p>
            <p><strong>Follwing: </strong>{{userProfile.following}}</p>
            <p><strong>Public Repos: </strong>{{userProfile.public_repos}}</p>
            

        </div>
    </div>
    <div v-if="error" class="error-message">
     <p>{{ error }}</p>
    </div>

</template>




<style>
.github-profile {
  max-width: 600px;
  margin: 0 auto;
  padding: 24px;
  background-color: white;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  border-radius: 8px;
  margin-top:100px;
}

.app-title {
  font-size: 24px;
  font-weight: bold;
  text-align: center;
  margin-bottom: 24px;
  color: #333;
}

.input-container input {
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 6px;
  outline: none;
}

.input-container input:focus {
  border-color: #007bff;
}

.user-profile {
  margin-top: 24px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.user-profile img {
  width: 120px;
  height: 120px;
  border-radius: 50%;
  margin-bottom: 16px;
}

.user-details {
  text-align: left;
  width: 100%;
}

.user-details p {
  font-size: 16px;
  margin: 8px 0;
}

.error-message {
  margin-top: 16px;
  color: red;
  font-size: 16px;
}

  
</style>


