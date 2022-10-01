<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
  import contacts from './contacts.json';
  import { reactive } from 'vue';

  const ironContacts = reactive(contacts.splice(0,5));
  const oscarTrophy = "https://assets.stickpng.com/images/580b585b2edbce24c47b2d48.png";
  const emmyTrophy = "https://assets.stickpng.com/images/5853c5a6ec0c270fc2f62dfd.png"

  function addContact() {
    const position = Math.floor(Math.random()*contacts.length);
    const removeRandomContact = contacts.splice(position, 1);
    const randomContact = removeRandomContact.pop();

    ironContacts.push(randomContact);
  };
</script>

<template>
  <h1>IronContacts</h1>
  <button @click="addContact" type="button">Add Random Contact</button>
  <table>
    <thead>
      <tr>
        <th>Picture</th>
        <th>Name</th>
        <th>Popularity</th>
        <th>Won an Oscar</th>
        <th>Won an Emmy</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="contact in ironContacts" :key="contact.id">
        <td> <img :src="contact.pictureUrl" /></td>
        <td> {{ contact.name }} </td>
        <td> {{ contact.popularity.toFixed(2) }} </td>
        <td v-if="contact.wonOscar"><img :src="oscarTrophy" class="premio"/></td>
        <td v-else></td>
        <td v-if="contact.wonEmmy"> <img :src="emmyTrophy" class="premio"/> </td>
        <td v-else></td>
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

  table {
    margin: auto;
  }

  img {
    width: 70px;
    height: auto;
  }

  .premio {
    width: 30px;
    height: auto;
  }
</style>
