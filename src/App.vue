<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import HelloWorld from "./components/HelloWorld.vue";
import contacts from "./contacts.json";
import { ref } from "vue";

defineProps({
  contacts: Object,
});

const title = "IronContacts";
const fiveContacts = ref(contacts.slice(0,5));


const picker = () => { 
   let otherRandomContact = contacts[Math.floor(Math.random() * contacts.length)];
   if (fiveContacts.value.includes(otherRandomContact)) {
     return;
   } else {
    fiveContacts.value.push(otherRandomContact);
   }
 };


 const sortByName = () => {
 return fiveContacts.value.sort((a, b) => {
     if (a.name < b.name) {
       return -1;
     }
     if (a.name > b.name) {
       return 1;
     }
     return 0;
   });

}


const sortByPopularity = () => {
  return fiveContacts.value.sort((a, b) => {
     if (a.popularity > b.popularity) {
       return -1;
     }
     if (a.popularity < b.popularity) {
       return 1;
     }
     return 0;
   });
}


const removeContacts = (contactName) => { 
  fiveContacts.value.forEach((contact, index) =>{
     if (contact.id === contactName) {
      fiveContacts.value.splice(index, 1);
       return fiveContacts;
     }
   });
 }

</script>

<template>
  <div >
    <div class="app">{{ title }}</div>

    <div class ="topButtons">
      <button @click="picker"> Add Random Contact</button>
      <button @click="sortByPopularity" class ="btn"> Sort by popularity</button>
      <button @click="sortByName"> Sort by name</button>
    </div>
<div class ="topButtons">
    <table >
      <tr >
        <th>Picture</th>
        <th class ="btn">Name</th>
        <th >Popularity</th>
        <th>Won <br>Oscar</th>
        <th class ="btn">Won <br>Emmy</th>
        <th>Actions</th>
      </tr>

      <tr v-for="(contact, index) in fiveContacts" key="index">
        <td > <img :src="contact.pictureUrl" alt="profile pic"></td>
        <td >{{contact.name}}</td>
        <td>{{contact.popularity}}</td>
        <td v-if ="contact.wonOscar">🏆</td>
        <td v-else ></td>
        <td v-if ="contact.wonEmmy">🏆</td>
        <td v-else ></td>
        <td @click="removeContacts(contact.id)"><button>Delete</button></td>
      </tr>

    </table>
  </div>
  </div>
</template>

<style>
.app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  font-size: 40px;
}


img{ 
  width: 50px;}

.topButtons{
  display: flex;
  justify-content: center;
  margin: 20px
}

.btn {
  margin-left: 10px;
  margin-right: 10px;
}

</style>
