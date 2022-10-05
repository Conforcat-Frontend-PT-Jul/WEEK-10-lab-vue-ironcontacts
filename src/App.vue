<script setup>
import contacts from "./contacts.json";
import { ref } from "vue";

const showingContacts = ref(contacts.slice(0, 5));

function addContact() {
  const randomContact = contacts[Math.floor(Math.random() * contacts.length)];
  if (!showingContacts.value.includes(randomContact)) {
    return showingContacts.value.unshift(randomContact);
  } else {
    return addContact();
  }
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
  <nav>
    <h1>IronContacts</h1>
    <container class="buttons">
      <button @click="addContact" type="button">Add Random Contact</button>
      <button @click="sortContacts" type="button">Sort by name</button>
      <button @click="sortPopularity" type="button">Sort by popularity</button>
    </container>
  </nav>
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
        <TransitionGroup name="list">
          <td>
            <img :src="contact.pictureUrl" alt="{{contact.id}}" class="star" />
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
        </TransitionGroup>
      </tr>
    </tbody>
  </table>
</template>

<style>
body {
  padding: 0px;
  margin: 0px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: antiquewhite;
  margin-top: 60px;
  background-image: url("./../public/background.jpg");

  background-size: cover;
  height: -webkit-fill-available;
  width: -webkit-fill-available;
  margin: 0;
  padding-bottom: 75px;
}

nav {
  position: sticky;
  top: 0px;
  background-image: url("./../public/background.jpg");
  z-index: 1;
  padding-bottom: 10px;
}

.buttons {
  display: flex;
  justify-content: space-evenly;
  margin-bottom: 20px;
}

img {
  width: 75px;
  border-radius: 5px;
  transition: all 0.5s ease-in-out;
  -webkit-transition: all 0.4s;
}

img:hover {
  transform: scale(1.9);
  translate: 600px;
  rotate: 360deg;
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

td {
  font-size: 20px;
  font-weight: 500;
}

button {
  position: relative;
  display: inline-block;
  padding: 15px 25px;
  background-color: gold;
  background-image: linear-gradient(gold, lightgoldenrodyellow);
  text-decoration: none;
  color: #2c3e50;
  border-style: none;
  border-radius: 10px;
  margin: 3px;
  font-size: 25px;
  font-family: sans-serif;
  font-weight: 100;
}
button:hover {
  background-color: lightgoldenrodyellow;
  background-image: linear-gradient(lightgoldenrodyellow, gold);
  cursor: pointer;
}

.list-move,
.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}

.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}

.list-leave-active {
  position: absolute;
}

h1 {
  margin-top: 0;
  padding: 35px;
}
</style>
