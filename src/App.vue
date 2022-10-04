<script setup>
import contacts from "./contacts.json";
import { ref } from "vue";

const showingContacts = ref(contacts.slice(0, 5));

function addContact() {
  const randomContact = contacts[Math.floor(Math.random() * contacts.length)];
  showingContacts.value.unshift(randomContact);
}

function sortContacts() {
  // showingContacts.value.sort((a, b) => a.name.localeCompare(b.name));
  showingContacts.value.sort((a, b) => {
    if (a.name < b.name) {
      return -1;
    } else if (a.name > b.name) {
      return 1;
    } else {
      return 0;
    }
  });
}

function sortPopularity() {
  showingContacts.value.sort((a, b) => b.popularity - a.popularity);
}

function deleteContact(id) {
  showingContacts.value.forEach((el, index) => {
    if (el.id === id) {
      showingContacts.value.splice(index, 1);
    }
  });
}
</script>

<template>
  <h1>IronContacts</h1>
  <button @click="addContact" type="button">Add Random Contact</button>
  <button @click="sortContacts" type="button">Sort Contacts by Name</button>
  <button @click="sortPopularity" type="button">
    Sort Contacts by Popularity
  </button>
  <table>
    <thead>
      <tr>
        <th>Picture</th>
        <th>Name</th>
        <th>Popularity</th>
        <th>Won Oscar</th>
        <th>Won Emmy</th>
        <th></th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="contact in showingContacts" :key="contact.id">
        <td>
          <img :src="contact.pictureUrl" alt="{{contact.id}}" />
        </td>
        <td>{{ contact.name }}</td>
        <td>{{ contact.popularity.toFixed(2) }}</td>
        <td v-if="contact.wonOscar" class="trophy">🏆</td>
        <td v-else></td>
        <td v-if="contact.wonEmmy" class="trophy">🌟</td>
        <td v-else></td>
        <td>
          <button @click="deleteContact(contact.id)" type="button">
            Delete
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
  width: 75px;
}

table {
  margin: 20px;

  width: -webkit-fill-available;
}

thead {
  font-weight: 800;
  font-size: x-large;
}

.trophy {
  font-size: 30px;
}
</style>
