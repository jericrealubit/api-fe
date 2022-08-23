
<template>
  <h1>{{profiles.length}}</h1>
  <ul>
    <li v-for="profile in profiles" align="left">
      <img :src="profile.imageUrl" alt="" width="50">
      {{ profile._id }} 
      {{ profile.username }}
      {{profile.imageUrl}}
      <a href="#" @click="getDoc(profile._id)">Edit</a> | 
      <a href="#" @click="deleteDoc(profile._id)">Delete</a>
    </li>
  </ul>    
  <hr>
  <input type="text" placeholder="username" v-model="formValues.username">
  <input type="text" placeholder="email" v-model="formValues.email">
  <input type="text" placeholder="imageUrl" v-model="formValues.imageUrl">
  <button @click="insertDoc">Insert</button>  
  <button @click="updateDoc">Update</button>
</template>

<script>
  const api = "https://rest-api-express-mongodb.netlify.app/.netlify/functions/api/" 
  export default {
    data() {
      return {
        profiles: [],
        id: "",
        formValues: {
          username: '',
          email: '',
          imageUrl: ''
        }
      }
    },
    methods: {      
      insertDoc() { // done
        fetch(api, {
            method: 'POST',
            headers: {
              'Content-Type': 'application/json'
            },
            body: JSON.stringify(this.formValues)            
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
            body: JSON.stringify(this.formValues)
          })
          .then((response) => response.text())
          .then((data) => {
            console.log(data)
          })
          .catch((err) => {
            if (err) throw err;
          })        
      },
      getDoc(id) { // done      
        this.id = id
        fetch(api + id, {
            method: 'GET'
          })
          .then((response) => response.json())
          .then((data) => {
            console.log(data)
              this.formValues.username = data.username
              this.formValues.email = data.email
              this.formValues.imageUrl = data.imageUrl
          })
          .catch((err) => {
            if (err) throw err;
          })
      },
      deleteDoc(id) { // done
        fetch(api + id, {
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

