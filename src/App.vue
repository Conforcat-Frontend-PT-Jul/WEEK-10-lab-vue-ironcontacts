<script setup>
import contacts from "./contacts.json";
import { ref } from "vue";

const first5contacts = ref(contacts.slice(0, 5));
function addRandomOtherContacts() {
  let otherRandomContact = contacts[Math.floor(Math.random() * contacts.length)];
  if (first5contacts.value.includes(otherRandomContact)) {
    return;
  } else {
    first5contacts.value.push(otherRandomContact);
  }
};

function sortByName() {
  first5contacts.value.sort((a, b) => a.name.localeCompare(b.name));
  return first5contacts;
};

function sortByPopularity() {
  first5contacts.value.sort((a, b) => b.popularity - a.popularity)
  return first5contacts;
};

function removeContacts(contactName) {
  first5contacts.value.forEach((contact, index) => {
    if (contact.id === contactName) {
      first5contacts.value.splice(index, 1);
      return first5contacts;
    }
  })
}
</script>

<template>
  <div class="app">
    <header>
      <h1 class="title">IronContacts</h1>
      <div class="buttons">
        <button @click="addRandomOtherContacts">Add Random Contacts</button>
        <button @click="sortByName">Sort by Name</button>
        <button @click="sortByPopularity">Sort by Popularity</button>
      </div>
    </header>
    <table class="table">
      <thead>
        <tr>
          <th>Picture</th>
          <th>Name</th>
          <th>Popularity</th>
          <th>Won Oscar</th>
          <th>Won Emmy</th>
          <th>Actions</th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="contact in first5contacts" :key="contact.id">
          <td><img :src="contact.pictureUrl"></td>
          <td>{{ contact.name }}</td>
          <td>{{ contact.popularity.toFixed(2) }}</td>
          <td v-if="contact.wonOscar">🏆</td>
          <td v-else></td>
          <td v-if="contact.wonEmmy">🌟</td>
          <td v-else></td>
          <td><button @click="removeContacts(contact.id)">Delete</button></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style>
#app {
  color: black;
  margin-top: 50px;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 20px;
}

h1 {
  text-align: center;
  font-size: 46px;
  font-weight: bold;
  font-family: Arial, Helvetica, sans-serif;
  color: black;

}

.buttons {
  display: flex;
  justify-content: space-around;
  margin: 20px 10px 30px 10px;
}

.table {
  text-align: center;
  width: 90%;
  margin: auto;
}

img {
  width: 70px;
}
</style>
