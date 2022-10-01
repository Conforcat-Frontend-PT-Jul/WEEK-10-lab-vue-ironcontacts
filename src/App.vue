<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
  import contacts from './contacts.json';
  import { reactive } from 'vue';

  const fiveFirstContacts = reactive(contacts.slice(0,5));

</script>

<template>
  <h1>IronContacts</h1>
  <table>
    <thead>
      <tr>
        <th>Picture</th>
        <th>Name</th>
        <th>Popularity</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="contact in fiveFirstContacts" :key="contact.id">
        <td> <img :src="contact.pictureUrl" /></td>
        <td> {{ contact.name }} </td>
        <td> {{ contact.popularity}} </td>
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
</style>
