<script setup>
import contacts from '../src/contacts.json'
import { ref } from "vue";

let fiveContacts = ref(contacts.slice(0, 5));
console.log(fiveContacts);

function addRandomContact() {
  let randomContact = contacts[Math.floor(Math.random() * contacts.length)];
  if (fiveContacts.value.includes(randomContact)) {
    return;
  } else {
    fiveContacts.value.push(randomContact);
  }
}

function sortByPopularity() {
  fiveContacts.value.sort((a, b) => b.popularity - a.popularity);
  return fiveContacts;
}

function sortByName() {
  fiveContacts.value.sort((a, b) => a.name.localeCompare(b.name));
  return fiveContacts;
}

function deleteContact(id) {
  console.log(id);
  fiveContacts.value.forEach((contact, index) => {
    if (contact.id === id) {
      fiveContacts.value.splice(index, 1);
      return fiveContacts;
    }
  });
}
</script>


<template>
  <div id="app">
    <div id="web-mode">
      <img class="sun" src="./assets/sun.png" />
      <label class="mode-switch">
        <input type="checkbox" />
        <span class="slider"></span>
      </label>
      <img class="moon" src="./assets/moon.png" />
    </div>
    <div id="header">
      <p>🌟 IronContacts 🌟</p>
      <button class="btn-sort" @click="addRandomContact()">
        Add Random Contact
      </button>
      <button class="btn-sort" @click="sortByPopularity()">
        Sort by popularity
      </button>
      <button class="btn-sort" @click="sortByName()">Sort by name</button>
    </div>

    <table>
      <tr>
        <th>Picture</th>
        <th>Name</th>
        <th>Popularity</th>
        <th>Won an Oscar</th>
        <th>Won an Emmy</th>
        <th>Actions</th>
      </tr>
      <tr v-for="contact in fiveContacts">
        <td><img :src="contact.pictureUrl" /></td>
        <td>{{ contact.name }}</td>
        <td>{{ contact.popularity.toFixed(2) }}</td>
        <td v-if="contact.wonOscar">🏆</td>
        <td v-else="contact.wonOscar"></td>
        <td v-if="contact.wonEmmy">🌟</td>
        <td v-else="contact.wonEmmy"></td>
        <td><button class="deletetor" @click="deleteContact(contact.id)">Delete</button></td>
      </tr>
    </table>
  </div>
</template>

<style>
p {
  font-size: 2rem;
  font-weight: 700;
  font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
}

img {
  width: 80px;
}

table {
  text-align: center;
  border-spacing: 20px;
  border-spacing: 20px;
  margin-left: auto;
  margin-right: auto;
  font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
}

#header {
  text-align: center;
}

.btn-sort {
  margin-left: 20px;
  border: none;
  background-color: brown;
  color: aliceblue;
  padding: 10px;
  font-weight: bold;
  cursor: pointer;
}

.btn-sort:hover {
  background-color: rgb(204, 81, 81);
  transform: scale(1.2);
}

.deletetor {
  background-color: blueviolet;
  color: aliceblue;
  border: none;
  padding: 10px;
  font-weight: bold;
  cursor: pointer;
}

.deletetor:hover {
  background-color: rgb(189, 131, 244);
  transform: scale(1.2);
}

#web-mode {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 30px 0px;
}

#web-mode .sun {
  height: 35px;
  width: 35px;
}

#web-mode .moon {
  height: 35px;
  width: 35px;
  margin-left: 5px;
}

.mode-switch {
  position: relative;
  width: 45px;
  height: 28px;
}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  transition: 0.4s;
  border-radius: 51px;
}

.slider:before {
  position: absolute;
  content: "";
  height: 25px;
  width: 25px;
  top: 1px;
  bottom: 2px;
  background-color: white;
  -webkit-transition: 0.4s;
  transition: 0.4s;
  border-radius: 50%;
}

input:checked+.slider {
  background-color: #072ac8;
}

input:checked+.slider:before {
  transform: translateX(25px);
}

</style>