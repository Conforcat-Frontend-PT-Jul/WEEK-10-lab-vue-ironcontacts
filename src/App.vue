<template>
  <div class="app">
    <h1>IRON CONTACTS</h1>
    <button @click="addContact" type="button">Add Random Contact</button>
    <button @click="sortName" type="button">Sort by name</button>
    <button @click="sortPopularity" type="button">Sort by popularity</button>
    <table>
      <tr>
        <th>Picture</th>
        <th>Name</th>
        <th>Popularity</th>
        <th>Won Oscar</th>
        <th>Won Emmy</th>
        <th>Actions</th>
      </tr>
      <tr  v-for="(contact, index) in contacts" :key="index">
        <td><img :src="contact.pictureUrl" alt="contact picture"  style="width: 150px"/></td>
        <td>{{contact.name}}</td>
        <td>{{contact.popularity}}</td>
        <td v-if="contact.wonOscar"><img :src="trophy" style="width: 50px"/></td>
        <td v-if="contact.wonEmmy"><img :src="trophy" style="width: 50px"/></td>
        <td><button @click="deleteContact(contact.id)" type="button">Delete</button></td>
      </tr>
    </table>
  </div>
</template>

<script setup>
import data from './contacts.json'
import {ref} from 'vue'

let contacts = ref(data.splice(0,5));
const trophy = "https://emojipedia-us.s3.dualstack.us-west-1.amazonaws.com/thumbs/160/apple/325/trophy_1f3c6.png";

const addContact = function(){
  const random = Math.random()*data.length;
  const getContact = data.splice(random, 1);
  const newContact = getContact.pop();  
  contacts.value.push(newContact);
};

const sortName = function () {  
  contacts.value.sort((a,b) =>  a.name.localeCompare(b.name));
}

const sortPopularity = function () {
  contacts.value.sort((a,b) => {
    return a.popularity - b.popularity;
  })
}

const deleteContact = function (id) {
  contacts.value.forEach((contact, index) => {
    if(contact.id === id){
      contacts.value.splice(index, 1)
      data.push(contact);
    }
  })
}


</script>

<style>

</style>