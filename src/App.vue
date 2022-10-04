<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import contacts from "./contacts.json";
import { ref } from "vue";
const firstFiveContacts = contacts.slice(0, 6);
const randomContact = ref("");
</script>

<template>
  <div class="contact-card">
    <h1>Iron Contacts</h1>
    <table>
      <tr>
        <th>Picture</th>
        <th>Name</th>
        <th>Popularity</th>
        <th>Won an Oscar</th>
        <th>Won an Emmy</th>
      </tr>
      <tr v-for="contact in firstFiveContacts" :key="contact.id">
        <td>
          <img class="contact-image" :src="contact.pictureUrl" alt="foto" />
        </td>
        <td>{{ contact.name }}</td>
        <td>{{ contact.popularity.toFixed(2) }}</td>
        <td v-if="contact.wonOscar">🏆</td>
        <td v-else></td>
        <td v-if="contact.wonEmmy">🏆</td>
        <td v-else></td>
      </tr>
    </table>
    <button>Add Random Contact</button>
  </div>
</template>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins&display=swap");
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: Arial, Helvetica, sans-serif;
}

.contact-image {
  width: 80px;
}

.contact-card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  width: 50%;
  margin: 3em auto;
  padding: 3em;
}
</style>
