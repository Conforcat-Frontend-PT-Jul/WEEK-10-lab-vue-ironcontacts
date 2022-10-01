<script setup>
//import HelloWorld from './components/HelloWorld.vue'
import { reactive } from 'vue'
import contacts from "./contacts.json";

let currentContact = reactive(
  {
    "name": "",
    "pictureUrl": "",
    "popularity": "",
    "id": "",
    "wonOscar": "",
    "wonEmmy": ""
  }

);

function add() {
  const min = 5;
  const max = contacts.length - 1;
  const toAdd = Math.floor(Math.random() * (max - min + 1) + min);
  console.log("Add Clicked!!!", max);
  console.log(toAdd);
  currentContact = {
    "name": contacts[toAdd].name,
    "pictureUrl": contacts[toAdd].pictureUrl,
    "popularity": contacts[toAdd].popularity,
    "id": contacts[toAdd].id,
    "wonOscar": contacts[toAdd].wonOscar,
    "wonEmmy": contacts[toAdd].wonEmmy
  }

  console.log("Random:\n", currentContact);
}
</script>

<template>
  <!-- <HelloWorld /> -->
  <h1>IronContacts</h1>
  <div>
    <button @click="add()">Add random</button>
  </div>
  <table>
    <tr>
      <th>Pcture</th>
      <th>Name</th>
      <th>Popularity</th>
      <th>Won Oscar</th>
      <th>Won Emmy</th>
    </tr>

    <tr v-for="index in 5" :key="index">
      <td><img :src="contacts[index-1].pictureUrl"></td>
      <td :name="name">{{contacts[index-1].name}}</td>
      <td>{{contacts[index-1].popularity}}</td>
      <td v-if="contacts[index-1].wonOscar">
        <img class="icon" src="./assets/oscar.png">
      </td>
      <td v-else></td>
      <td v-if="contacts[index-1].wonEmmy">
        <img class="icon" src="./assets/emy.png">
      </td>
      <td v-else></td>
    </tr>


    <!--
    <tr v-for="contact in contacts" :key="contact.id">
      <td>{{contact.pictureUrl}}</td>
      <td>{{contact.name}}</td>
      <td>{{contact.popularity}}</td>
      <td>{{contact.wonOscar}}</td>
      <td>{{contact.wonEmmy}}</td>
    </tr>  -->
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

div {
  margin-bottom: 20px;
}

img {
  height: 40px;
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
  text-align: left;
  background-color: #0489aa;
  color: white;
}

.icon {
  width: 30px;
  height: 30px;

}
</style>
