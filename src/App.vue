<script setup>
import allContacts from './contacts.json'
import { onMounted, ref } from 'vue';

const contacts = ref([]);
let i;

for(i=0; i<5; i++) {
  contacts.value.push(allContacts[i])
}

//console.log(contacts.value[0])


</script>

<template>
  <header>
    <h1>IronContacts</h1>
  </header>
  <table>
    <tr>
      <th>Picture</th>
      <th>Name</th>
      <th>Popularity</th>
      <th>Won and Oscar</th>
      <th>Won an Emmy</th>
    </tr>
    <tr v-for="contact in contacts" :key="contacts.name">
      <td>
        <img alt="Celebrity picture" :src=contact.pictureUrl>
      </td>
      <td> {{ contact.name }} </td>
      <td> {{ contact.popularity }} </td>
      <td> {{ contact.name }} </td>
      <td> {{ contact.popularity }} </td>
    </tr>
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

td img {
 width: 100px ;
}
</style>
