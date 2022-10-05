<script setup>
import contacts from "./contacts.json"
import { ref, } from "vue"

const firstContacts = ref(contacts.slice(0, 5)) 

function addRandomContact() {
  let randomContact = contacts[Math.floor(Math.random() *contacts.length)] //www.w3resource.com/javascript-exercises/javascript-array-exercise-35.php Revisar//

  if (firstContacts.value.includes(randomContact) ){
    return;
  } else {
    firstContacts.value.push(randomContact)
  }
};  

function sortByName() {
  firstContacts.value.sort( function(a, b ) {
    return a.name < b.name ? -1 : a.name > b.name ? 1 : 0; 
  })
}

function sortByPopularity() {
  firstContacts.value.sort( function(a, b) {
    return a.popularity < b.popularity ? 1 : a.popularity > b.popularity ? -1 : 0;
  })
}

function deleteContact(id) {
  
  firstContacts.value.forEach((contact, index) => { 
    if (contact.id === id) {
    firstContacts.value.splice(index, 1)
    return firstContacts
    }
  })
  

}

</script>

<template> 
  <div id="app">
    <div id="header">
      <p class="fs-2">Iron Contacts</p>
      <button type="button" class="m-2 btn btn-outline-secondary btn-sm" @click="sortByName">Sort by name</button> 
      <button type="button" class="m-2 btn btn-outline-secondary btn-sm" @click="sortByPopularity">Sort by popularity</button> 
      <button type="button" class="m-2 btn btn-outline-secondary btn-sm" @click="addRandomContact">Add Random Contact</button>  
    </div>
    <table class="table">
      <tr>
        <th>Picture</th>
        <th>Name</th>
        <th>Popularity</th>
        <th>Won an Oscar</th>
        <th>Won an Emmy</th>
        <th>Actions</th>
      </tr>
      <tr v-for="contacts in firstContacts">
        <td><img :src="contacts.pictureUrl" alt=""></td>
        <td>{{ contacts.name }}</td>
        <td>{{ contacts.popularity.toFixed(2) }}</td>
        <td v-if="contacts.wonOscar">🏆</td>
        <td v-if="contacts.wonEmmy">🏆</td>
        <td><button type="button" class="btn btn-outline-secondary btn-sm" @click="deleteContact(contact.id)">Delete</button></td>
      </tr>
    </table>
  </div>

</template>

<style>


img {
    width: 90px;
  }
#app {

  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
