<script setup>
import contacts from "./contacts.json";

import { ref } from "vue";

const fiveContacts = ref(contacts.slice(0, 10));

console.log(fiveContacts);
</script>

<template>
  <div id="app">
    <table>
      <tr>
        <th>Picture</th>
        <th>Name</th>
        <th>Popularity</th>
        <th>Won an Oscar</th>
        <th>Won an Emmy</th>
      </tr>
      <tr v-for="contact in fiveContacts">
        <td><img :src="contact.pictureUrl" /></td>
        <td>{{ contact.name }}</td>
        <td>{{ contact.popularity }}</td>
        <td v-if="contact.wonOscar">🏆</td>
        <td v-else="contact.wonOscar"></td>
        <td v-if="contact.wonEmmy">🏆</td>
        <td v-else="contact.wonEmmy"></td>
      </tr>
    </table>
  </div>
</template>

<style>
img {
  width: 80px;
}

table {
  text-align: center;
  border-spacing: 20px;
  border-spacing: 20px;
}
</style>
