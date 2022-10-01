<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import contacts from "./contacts.json";
import { defineProps, ref } from "vue"

const contactsData = ref(contacts);


</script>

<template>
<div class="col-7" :contacts="contactsData" >
  <h1> Contactos</h1>
  <table class="table">
  <thead>
    <tr>
   
      <th scope="col">Picture</th>
      <th scope="col">Name</th>
      <th scope="col">Popularity</th>
      <th scope="col">wonEmmy</th>
      <th scope="col">wonOscar</th>
 
    </tr>
  </thead>  
</table>
  <table class="table" >

  <tbody>
    <tr v-for="contact in contacts.sort(name)" :key="contact.name">
      <td scope="row" class="row-td">
        <img :src="contact.pictureUrl" class="img-td" ></td>
      <td>{{ contact.name }}</td>
      <td>{{ parseInt(contact.popularity) }}</td>
      <td v-if="contact.wonEmmy === true">🏆</td>
      <td v-else="contact.wonEmmy === false ">💩</td>
      <td v-if="contact.wonOscar === true">🏆</td>
      <td v-else="contact.wonOscar === false ">💩</td>
    </tr>
  </tbody>
</table>
         </div>

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
.col-7{
  margin:0 auto;
}
.row-td{
  width: 10%;
}
.img-td{
  width: 100%;
}
</style>
