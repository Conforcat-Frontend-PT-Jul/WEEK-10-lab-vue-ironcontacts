<script setup>
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import HelloWorld from "./components/HelloWorld.vue";
import contacts from "./contacts.json";
import { ref } from "vue";

const fiveContacts = ref(contacts.slice(0, 5));
</script>

<template>
  <h1>IronContacts</h1>
  <table>
    <thead>
      <tr>
        <th>Picture</th>
        <th>Name</th>
        <th>Popularity</th>
        <th>Won Oscar</th>
        <th>Won Emmy</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="contact in fiveContacts" :key="contact.id">
        <td>
          <img :src="contact.pictureUrl" alt="{{contact.id}}" />
        </td>
        <td>{{ contact.name }}</td>
        <td>{{ contact.popularity.toFixed(2) }}</td>
        <td v-if="contact.wonOscar" class="trophy">🏆</td>
        <td v-if="contact.wonEmmy" class="trophy">🏆</td>
        <td v-else></td>
      </tr>
    </tbody>
  </table>
  <!-- <img alt="Vue logo" src="./assets/logo.png" /> -->

  <!-- <HelloWorld msg="Hello Vue 3 + Vite" /> -->
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

img {
  width: 75px;
}

table {
  /* padding: 10px 37%; */
  margin: auto;
}

thead {
  font-weight: 800;
  font-size: x-large;
}

.trophy {
  font-size: 30px;
}
</style>
