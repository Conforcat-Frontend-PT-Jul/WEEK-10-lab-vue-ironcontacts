<script setup>
import contacts from "./contacts.json";
import { ref } from "vue";

const movieContacts = ref(contacts.slice(0, 5));
</script>

<template>
  <div class="app"></div>
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
      <tr v-for="movieContact in movieContacts" :key="movieContact.id">
        <td>
          <img :src="movieContact.pictureUrl" alt="{{movieContact.id}}" />
        </td>
        <td>{{ movieContact.name }}</td>
        <td>{{ movieContact.popularity }}</td>
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
img {
  width: 100px;
  border-radius: 10px;
}
table {
  width: -webkit-fill-available;
}
h1 {
  font-size: 3em;
}
thead {
  font-size: 25px;
}
</style>
