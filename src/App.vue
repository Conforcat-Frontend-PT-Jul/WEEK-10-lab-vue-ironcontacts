<script setup>
import contacts from "./contacts.json";
import { ref } from "vue";

const movieContacts = ref(contacts.slice(0, 5));

function addRandomContact() {
  const randomContact = contacts[Math.floor(Math.random() * contacts.length)];
  if (movieContacts.value.includes(randomContact)) {
    return;
  } else {
    return movieContacts.value.unshift(randomContact);
  }
}
function sortByName() {
  movieContacts.value.sort((a, b) => a.name.localeCompare(b.name));
  return movieContacts;
}
function sortByPopularity() {
  movieContacts.value.sort((a, b) => b.popularity - a.popularity);
  return movieContacts;
}
function deleteContact(id) {
  movieContacts.value.forEach((el, index) => {
    if (el.id === id) {
      movieContacts.value.splice(index, 1);
    }
  });
}
</script>

<template>
  <div class="app"></div>
  <h1>IronContacts</h1>
  <button @click="addRandomContact()">Add Random Contact</button>
  <button @click="sortByName()">Sort by Name</button>
  <button @click="sortByPopularity()">Sort by Popularity</button>

  <table>
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
      <tr v-for="movieContact in movieContacts" :key="movieContact.id">
        <td>
          <img :src="movieContact.pictureUrl" alt="{{movieContact.id}}" />
        </td>
        <td>{{ movieContact.name }}</td>
        <td>{{ movieContact.popularity }}</td>
        <td v-if="movieContact.wonOscar">🏆</td>
        <td v-else></td>
        <td v-if="movieContact.wonEmmy">🏵</td>
        <td v-else></td>
        <td>
          <button @click="deleteContact(movieContact.id)">
            Delete Contact
          </button>
        </td>
      </tr>
    </tbody>
  </table>
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
img {
  width: 100px;
  border-radius: 10px;
}
table {
  width: -webkit-fill-available;
}
h1 {
  font-size: 3em;
}
thead {
  font-size: 25px;
  margin-bottom: 25px;
}
button {
  margin: 50px;
  width: 160px;
  height: 40px;
  color: whitesmoke;
  background-color: darkblue;
  font-weight: 800;
}
</style>
