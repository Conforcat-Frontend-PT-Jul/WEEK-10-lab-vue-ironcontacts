<script setup>
import { reactive } from 'vue'
import contacts from "./contacts.json";

let contactList = reactive([]);
for (let i = 0; i < 5; i++) {
  contactList.push(contacts[i]);
}

function add() {
  let min = contactList.length;  /* Min will change when I delete/add contacts from displayed list */
  const max = contacts.length - 1; /* Max won't change unless more items added in the json file */
  const toAdd = Math.floor(Math.random() * (max - min + 1) + min);
  contactList.push(contacts[toAdd]);
}

function remove(element) {
  const index = contactList.findIndex(object => {
    return object.id === element;
  });
  this.contactList.splice(index, 1);
}

function sortByName(){
  contactList.sort((a, b) => a.name.localeCompare(b.name));
}

function sortByPopularity(){
  contactList.sort((a, b) => (b.popularity - a.popularity));
}
</script>

<template>
  <h1>IronContacts</h1>
  <div>
    <button @click="add()">Add random</button>
    <button @click="sortByName()">Sort by Name</button>
    <button @click="sortByPopularity()">Sort by Popularity</button>
  </div>
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
      <tr v-for="contact in contactList" :key="contact.id">
        <td><img :src="contact.pictureUrl"></td>
        <td>{{contact.name}}</td>
        <td>{{contact.popularity.toFixed(2)}}</td>
        <td v-if="contact.wonOscar">
          <img class="icon" src="./assets/oscar.png">
        </td>
        <td v-else></td>
        <td v-if="contact.wonEmmy">
          <img class="icon" src="./assets/emy.png">
        </td>
        <td v-else></td>
        <td class="removeBtn"><img class="icon" @click="remove(contact.id)" src="./assets/bin.png"></td>
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
  margin-top: 10px;
}

div {
  margin-bottom: 20px;
}

img {
  height: 80px;
}

table {
  width: 70%;
  margin: auto;
}

td,
th {
  border: 1px solid #ddd;
  padding: 8px;
}

tr:nth-child(even) {
  background-color: #f2f2f2;
}

tr:hover {
  background-color: #ddd;
}

th {
  padding-top: 12px;
  padding-bottom: 12px;
  text-align: center;
  background-color: #0489aa;
  color: white;
}

.icon {
  width: 30px;
  height: 30px;

}

.removeBtn {
  margin: 0;
  cursor: pointer;
}

.removeBtn:hover {
  background-color: rgb(255, 96, 96);
}

button {
  background-color: #04aa78; /* Green */
  border: none;
  border-radius: 6px;
  color: white;
  padding: 15px 32px;
  text-align: center;
  font-weight: 700;
  display: inline-block;
  font-size: 18px;
  margin: 4px 10px;  
  cursor: pointer;
  transition-duration: 0.4s;
}

button:hover {
  box-shadow: 0 10px 12px 0 rgba(0,0,0,0.24),0 17px 50px 0 rgba(0,0,0,0.19);
  background-color: #0436aa; /* Green */
}
</style>
