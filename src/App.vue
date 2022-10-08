<template>
  <div class="app">
    <table>
      <tr>
        <th>Picture</th>
        <th>Name</th>
        <th>Popularity</th>
        <th>Won Oscar</th>
        <th>Won Emmy</th>
      </tr>
      <tr  v-for="(contact, index) in contacts" :key="index">
        <td><img :src="contact.pictureUrl" alt="contact picture"  style="width: 150px"/></td>
        <td>{{contact.name}}</td>
        <td>{{contact.popularity}}</td>
        <td v-if="contact.wonOscar"><img :src="trophy" /></td>
        <td v-if="contact.wonEmmy"><img :src="trophy" /></td>
      </tr>
    </table>
  </div>
</template>

<script setup>
import data from './contacts.json'
import {ref} from 'vue'

let contacts = ref(data.slice(0,5));
const trophy = "https://emojipedia-us.s3.dualstack.us-west-1.amazonaws.com/thumbs/160/apple/325/trophy_1f3c6.png";

console.log(contacts)


</script>

<style>

</style>