
<template>
  <h1>123</h1>
  <ul>
    <li v-for="profile in profiles">
      {{ profile.username }}
    </li>
  </ul>
  <button @click="insertDoc">Insert</button>
  <button @click="getDoc">Get</button>
  <button @click="deleteDoc">Delete</button>
  <button @click="updateDoc">Update</button>
</template>

<script>
  const api = "https://rest-api-express-mongodb.netlify.app/.netlify/functions/api/" 
  export default {
    data() {
      return {
        profiles: []
      }
    },
    methods: {
      insertDoc() {
        fetch(api, {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({
            // data you intend to send as JSON to the server                  
            "username": "fri",
            "email": "fri@gmail.com",
            "imageUrl": "https://drive.google.com/file/d/1hZfS5P7133Z64ylWcyPTs7PebV_EO_om/view?usp=sharing"            
          })
        })
      },
      getDoc() {
        fetch(api, {
          method: 'GET',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({
            // data you intend to send as JSON to the server                  
            "username": "fri",
            "email": "fri@gmail.com",
            "imageUrl": "https://drive.google.com/file/d/1hZfS5P7133Z64ylWcyPTs7PebV_EO_om/view?usp=sharing"            
          })
        })
      },
      deleteDoc() {
        fetch(api, {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({
            // data you intend to send as JSON to the server                  
            "username": "fri",
            "email": "fri@gmail.com",
            "imageUrl": "https://drive.google.com/file/d/1hZfS5P7133Z64ylWcyPTs7PebV_EO_om/view?usp=sharing"            
          })
        })
      },
      updateDoc() {
        fetch(api, {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({
            // data you intend to send as JSON to the server                  
            "username": "fri",
            "email": "fri@gmail.com",
            "imageUrl": "https://drive.google.com/file/d/1hZfS5P7133Z64ylWcyPTs7PebV_EO_om/view?usp=sharing"            
          })
        })
      }   
    },
    mounted() {      
      fetch(api)
        .then((response) => response.json())
        .then((data) => {
          this.profiles = data
        })
        .catch((err) => {
          if (err) throw err;
        })
    }
  }
</script>

