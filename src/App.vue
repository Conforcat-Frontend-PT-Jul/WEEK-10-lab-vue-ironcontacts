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
  
  firstContacts.value.forEach((key, index) => { 
    if (key.id === id) {
    firstContacts.value.splice(index, 1)[0]
    console.log(firstContacts.value.id) //firstContacts//
    }
  })
  

}

</script>

<template> 
  <div id="app" class>
    <div id="header">
      <p class="fs-2 my-0">Iron Contacts</p>
      <button type="button" class="mx-4 my-3 btn btn-secondary" @click="sortByName">Sort by name</button> 
      <button type="button" class="mx-4 my-3 btn btn-secondary" @click="sortByPopularity">Sort by popularity</button> 
      <button type="button" class="mx-4 my-3 btn btn-secondary" @click="addRandomContact">Add Random Contact</button>  
    </div>
    <div>
      <table class="table">
      <tr>
        <th>Picture</th>
        <th>Name</th>
        <th>Popularity</th>
        <th>Won an Oscar</th>
        <th>Won an Emmy</th>
        <th>Actions</th>
      </tr>
      <tr v-for="contact in firstContacts">
        <td><img :src="contact.pictureUrl" alt=""></td>
        <td>{{ contact.name }}</td>
        <td>{{ contact.popularity.toFixed(2) }}</td>
        <td v-if="contact.wonOscar">🏆</td>
        <td v-else="contact.wonOscar"></td>
        <td v-if="contact.wonEmmy">🏆</td>
        <td v-else="contact.wonEmmy"></td>
        <td><button type="button" class="btn btn-outline-danger" @click="deleteContact(contact.id)">Delete</button></td>
      </tr>
    </table>
    </div>
    
  </div>

</template>

<style>


img {
    width: 90px;
  }
#app {

  text-align: center;
  color: #2c3e50;
  margin-top: 30px;
  
}
#table {
 
  margin: auto;
  
  
 
}
</style>
