<script setup>
import contacts from "./contacts.json";

import { ref } from "vue";

const fiveContacts = ref(contacts.slice(0, 5));

console.log(fiveContacts);
</script>

<template>
  <div id="app">
    <table>
      <tr>
        <th>Picture</th>
        <th>Name</th>
        <th>Popularity</th>
      </tr>
      <tr v-for="contact in fiveContacts">
        <td><img :src="contact.pictureUrl" /></td>
        <td>{{ contact.name }}</td>
        <td>{{ contact.popularity }}</td>
      </tr>
    </table>
  </div>
</template>

<style>
img {
  width: 80px;
}
</style>
