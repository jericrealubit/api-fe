
<template>
  <h1>{{profiles.length}}</h1>
  <ul>
    <li v-for="profile in profiles" align="left">
      <img :src="profile.imageUrl" alt="" width="50">
      {{ profile._id }} 
      {{ profile.username }}
      {{profile.imageUrl}}
      <a href="#" @click="editDoc(profile._id)">Edit</a>
    </li>
  </ul>
  <input type="text" v-model.trim="id">{{id}}
  <button @click="insertDoc">Insert</button>
  <button @click="getDoc">Get</button>
  <button @click="deleteDoc">Delete</button>
  <button @click="updateDoc">Update</button>
  <hr>
  <input type="text" placeholder="username" v-model="formValues.username">
  <input type="text" placeholder="email" v-model="formValues.email">
  <input type="text" placeholder="imageUrl" v-model="formValues.imageUrl">
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
      editDoc(id) {        
        this.id = id;
        this.getDoc()        
      },
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
      getDoc() { // done
        fetch(api + this.id, {
            method: 'GET'
          })
          .then((response) => response.json())
          .then((data) => {
            console.log(data)
              this.formValues.username = data.username
              this.formValues.email =  data.email
              this.formValues.imageUrl =  data.imageUrl
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

