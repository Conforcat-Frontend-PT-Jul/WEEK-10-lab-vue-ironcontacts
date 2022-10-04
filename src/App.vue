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
        <!-- <TransitionGroup name="list" tag="td"> -->
        <td>
          <Transition>
            <img :src="contact.pictureUrl" alt="{{contact.id}}" class="star" />
          </Transition>
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
        <!-- </TransitionGroup> -->
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
  /* color: #2c3e50; */
  color: antiquewhite;
  margin-top: 60px;
  background-image: url("./../public/background.jpg");

  background-size: cover;
  height: -webkit-fill-available;
  width: -webkit-fill-available;
  margin: 0;
  padding-bottom: 75px;
}

img {
  width: 75px;
  border-radius: 5px;
  transition: all 0.5s ease-in-out;
  -webkit-transition: all 0.4s;
}

img:hover {
  transform: scale(1.3);
  translate: 500px;
  rotate: 360deg;
  /* margin-left: 800px; */
  /* position: absolute;
  right: 50%; */
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

.list-enter-active,
.list-leave-active {
  transition: all 1.5s ease;
}

.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}

.star-enter-active,
.star-leave-active {
  transition: opacity 0.5s ease;
}

.star-enter-from,
.star-leave-to {
  opacity: 0;
}
h1 {
  margin-top: 0;
  padding: 35px;
}
</style>
