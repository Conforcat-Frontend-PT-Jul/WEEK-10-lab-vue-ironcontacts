<script setup>
import { onMounted, ref } from "vue";
import contacts from "./contacts.json";

const arContacts = ref(null);

function obtenir5Contacts() {
  arContacts.value = contacts.slice(0, 5);
}

function addContact() {
  arContacts.value.push(contacts[Math.floor(Math.random() * (contacts.length - 0 + 1) + 0)]);
}

function sort(param) {
  switch (param) {
    case 'name':
      arContacts.value.sort(compareName);
      break;
    case 'popularity': 
      arContacts.value.sort(comparePopularity);
      break;
    default:
      break;
  }
}

function compareName(a, b) {
  if ( a.name < b.name ){
    return -1;
  }
  if ( a.name > b.name ){
    return 1;
  }
  return 0;
}

function comparePopularity(a, b) {
  if ( a.popularity > b.popularity ){
    return -1;
  }
  if ( a.popularity < b.popularity ){
    return 1;
  }
  return 0;
}

function deleteContact(index) {
  arContacts.value.splice(index, 1);
}

onMounted(() => {
  obtenir5Contacts();
})
</script>

<template>
  <div class="app">
    <table class="table">
      <thead class="table-header">
          <p class="title">IronContacts</p>
      </thead>
      <tbody>
        <tr class="add-btn">
          <button v-on:click="addContact">Add Random Contact</button>  
          <button v-on:click="sort('popularity')">Sort by popularity</button>  
          <button v-on:click="sort('name')">Sort by name</button>  
        </tr>
        <tr class="row">
          <td class="info subtitle">Picture</td>
          <td class="info subtitle">Name</td>
          <td class="info subtitle">Popularity</td>
          <td class="info subtitle">Won Oscar</td>
          <td class="info subtitle">Won Emmy</td>
          <td class="info subtitle">Actions</td>
        </tr>
        <tr v-for="(contact, index) in arContacts"  class="row">
          <td class="info">
            <img class="picture" :src="contact.pictureUrl" />
          </td>
          <td  class="info">
            <p class="info">{{contact.name}}</p>
          </td>
          <td  class="info">
            <p class="info">{{contact.popularity}}</p>
          </td>
          <td  class="info">
            <p v-if="contact.wonOscar">🏆</p>
          </td>
          <td  class="info">
            <p v-if="contact.wonEmmy">🏆</p>
          </td>
          <td  class="info">
            <button v-on:click="deleteContact(index)">Delete</button> 
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style>
.app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.table {
  width: 900px;
  margin: 0;

}

.add-btn {
  width: 900px;
  
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;
}

.add-btn button {
  margin-top: 20px;
  margin-bottom: 20px;
}

.table-header {
  display: table-caption;
}

.subtitle {
  font-size: large;
  font-weight: 600;
}

.title {
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 35px;
  font-weight: bold;
  width: 100%;
  padding: 0;
  margin: 0;
}

.row {
  display: flex;
  justify-content: space-around;
  align-items: center;
  width: 900px;
}

.info {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 150px;
}

.picture {
  width: 100px;
}
</style>
