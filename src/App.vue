<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import contacts from "./contacts.json";
import { ref } from 'vue'

const manyContacts = ref([]);

addRandomContact();
addRandomContact();
addRandomContact();
addRandomContact();
addRandomContact();

function addRandomContact() {
  if(contacts.length <= 0) {
    return;
  }

  const posContact = Math.floor(Math.random() * contacts.length);
  const randomContacts = contacts.splice(posContact, 1);
  manyContacts.value.push(randomContacts[0]);
}

function sortByPopularity() {
  manyContacts.value.sort((contactA, contactB) => contactB.popularity - contactA.popularity);
}

function sortByName() {
  manyContacts.value.sort((contactA, contactB) => {
    let nameContactA = contactA.name.toLowerCase();
    let nameContactB = contactB.name.toLowerCase();

    if (nameContactA < nameContactB) {
        return -1;
    }
    if (nameContactA > nameContactB) {
        return 1;
    }
    return 0;
  });
}

function deleteContact(id){
  const posContact = manyContacts.value.findIndex(contact => contact.id === id);
  const contactRemoved = manyContacts.value.splice(posContact,1);
  contacts.push(contactRemoved[0]);
}

</script>

<!-- src/App.js -->
<template>
  <div class="app">
    <h1>IronContacts</h1>
    <button @click="addRandomContact()">Add Random Contact</button>
    <button @click="sortByPopularity()">Sort by popularity</button>
    <button @click="sortByName()">Sort the table by name</button>
    <table>
      <thead>
        <th><h3>Picture</h3></th>
        <th><h3>Name</h3></th>
        <th><h3>Popularity</h3></th>
        <th><h3>Won Oscar</h3></th>
        <th><h3>Won Emmy</h3></th>
        <th><h3>Actions</h3></th>
      </thead>
      <tbody>
        <tr v-for="contact of manyContacts">
          <td><img :src="contact.pictureUrl"/></td>
          <td>{{ contact.name }}</td>
          <td>{{ contact.popularity.toFixed(2) }}</td>
          <td><span v-if="contact.wonOscar">&#127942;</span></td>
          <td><span v-if="contact.wonEmmy">&#127942;</span></td>
          <td><button @click="deleteContact(contact.id)">Delete</button></td>
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

button{
  margin:20px
}
 img{
  height: 100px;
  width: 70px;
 }

 h3{
  font-weight: bold;
 }

table{
  text-align: center;
  margin: auto;
}
</style>
