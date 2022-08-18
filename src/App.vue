
<template>
  <h1>{{profiles.length}}</h1>
  <ul>
    <li v-for="profile in profiles" align="left">
      <img :src="profile.imageUrl" alt="" width="150">
      {{ profile._id }} 
      {{ profile.username }}
      {{profile.imageUrl}}
    </li>
  </ul>
  <input type="text" v-model.trim="id">{{id}}
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
        profiles: [],
        id: ""
      }
    },
    methods: {
      insertDoc() { // done
        fetch(api, {
            method: 'POST',
            headers: {
              'Content-Type': 'application/json'
            },
            body: JSON.stringify({
              // data you intend to send as JSON to the server                  
              "username": "fri123",
              "email": "fri@gmail.com",
              "imageUrl": "https://drive.google.com/file/d/1hZfS5P7133Z64ylWcyPTs7PebV_EO_om/view?usp=sharing"            
            })
          })
          .then((response) => response.text())
          .then((data) => {
            console.log(data)
          })
          .catch((err) => {
            if (err) throw err;
          })
      },
      updateDoc() {
        fetch(api + this.id, {
            method: 'PUT',
            headers: {
              'Content-Type': 'application/json'
            },
            body: JSON.stringify({              
              "username": "satfrisun",
              "email": "fri@gmail.com",
              "imageUrl": "https://freeimage.host/i/gYiWOJ"            
            })
          })
          .then((response) => response.text())
          .then((data) => {
            console.log(data)
          })
          .catch((err) => {
            if (err) throw err;
          })        
      },
      getDoc() { // done
        fetch(api + this.id, {
            method: 'GET'
          })
          .then((response) => response.text())
          .then((data) => {
            console.log(data)
          })
          .catch((err) => {
            if (err) throw err;
          })
      },
      deleteDoc() { // done
        fetch(api + this.id, {
            method: 'DELETE'           
          })
          .then((response) => response.text())
          .then((data) => {
            console.log(data)
          })
          .catch((err) => {
            if (err) throw err;
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

