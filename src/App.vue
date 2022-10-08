<template>
  <div class="app">
    <table>
      <tr>
        <th>Picture</th>
        <th>Name</th>
        <th>Popularity</th>
      </tr>
      <tr  v-for="(contact, index) in contacts" :key="index">
        <td><img :src="contact.pictureUrl" alt="contact picture"  style="width: 150px"/></td>
        <td>{{contact.name}}</td>
        <td>{{contact.popularity}}</td>
      </tr>
    </table>
  </div>
</template>

<script setup>
import data from './contacts.json'
import {ref} from 'vue'

let contacts = ref(data.slice(0,5));
console.log(contacts)


</script>

<style>

</style>