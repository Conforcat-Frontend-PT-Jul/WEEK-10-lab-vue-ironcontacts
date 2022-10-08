<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import contacts from "./contacts.json";
import { ref } from "vue"


const contactsData = ref(contacts.splice(0,5));

const addRandom = () => {
  contactsData.value.unshift(contacts[
  Math.floor(Math.random() * contactsData.value.length)
  ])
};

const deleteContact = () => {
  contactsData.value.splice(0,1);
};

const sortByName = () => {
     contactsData.value.sort((a, b) => {
        if (a.name > b.name) return 1;
        else return -1;
      });
    };

const sortByPop = () => {
     contactsData.value.sort((a, b) => {
        if (a.popularity > b.popularity) return -1;
        if( a.popularity < b.popularity) return  1;
        else return 0;
      });
    };
</script>

<template>
<div class="col-7"  >
  <h1> Contactos</h1>
  <button @click="addRandom">Add a random profile</button>
  <button @click="sortByPop">Sort By Popularity</button>
  <button @click="sortByName">Sort By Name</button>
  <table class="table">
    
  <thead>
    <tr class="row-td">
      <th scope="col ">#</th>
      <th scope="col">Picture</th>
      <th scope="col"></th>
      <th scope="col"></th>
      <th scope="col"></th>
      <th scope="col">Full Name</th>
      <th scope="col"></th>
      <th scope="col">Popularity</th>
      <th scope="col">wonEmmy</th>
      <th scope="col">wonOscar</th>
    </tr>
  </thead>  
</table>
  <table class="table" >
  <tbody>
    <tr v-for="(contact, id ) in contactsData" :key="contact.name">
      <button @click="deleteContact(id)">X</button>
      <td scope="row" class="row-td">
      <img :src="contact.pictureUrl" class="img-td" ></td>
      <td>{{ contact.name }}</td>
      <td>{{ contact.popularity.toFixed(2) }}</td>
      <td v-if="contact.wonEmmy === true">🏆</td>
      <td v-else="contact.wonEmmy === false ">💩</td>
      <td v-if="contact.wonOscar === true">🏆</td>
      <td v-else="contact.wonOscar === false ">💩</td>
    </tr>
  </tbody>
  
</table>

         </div>

</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.col-7{
  margin:0 auto;
}
.row-td{
  width: 10%;
}
.img-td{
  width: 100%;
}



.table > :not(caption) > * > * {
    padding: 3.5rem 1.5rem;

  }
</style>
