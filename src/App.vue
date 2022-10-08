<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
/*import HelloWorld from './components/HelloWorld.vue'*/
import contacts from "./contacts.json";
import { ref } from "vue";

const first5contacts = ref(contacts.slice(0,5)); /* Iteration 1*/

function addRandomOtherContacts () { /*Iteration 3 formula to get ramdom contacts */
  let otherRandomContact = contacts[Math.floor(Math.random() * contacts.length)];
  if (first5contacts.value.includes(otherRandomContact)) {
    return;
  } else {
    first5contacts.value.push(otherRandomContact);
  }
};

function sortByName () { /*Iteration 4.1 Sort by Name Alphabeticaly*/
  first5contacts.value.sort((a,b) => a.name.localeCompare(b.name));
  return first5contacts;
};

function sortByPopularity () { /*Iteration 4.2 Sort by Name Alphabeticaly*/
  first5contacts.value.sort((a,b) => b.popularity - a.popularity)
  return first5contacts;
};

function removeContacts (contactName) { /*Iteracion 5 Delete button*/
  first5contacts.value.forEach((contact, index) =>{
    if (contact.id === contactName) {
      first5contacts.value.splice(index, 1);
      return first5contacts;
    }
  })
}

</script>

<!-- src/App.js -->
<template>
  <div class="app">
    <header>
      <h1 class = "title">Iron Contacts</h1>
      <div class = "buttons">
        <button @click="addRandomOtherContacts">Add Random Contacts</button>
        <button @click="sortByName">Sort by Name</button>
        <button @click="sortByPopularity">Sort by Popularity</button>
      </div>
    </header>
    <table class ="tablewithinfo">
      <thead>
        <tr>
          <th>Picture</th>
          <th>Name</th>
          <th>Popularity</th>
          <th>Won Oscar</th>
          <th>Won Emmy</th>
          <th>Actions</th> <!--Iteration 5-->
        </tr>
      </thead>
      <tbody>
        <tr v-for="contact in first5contacts" :key="contact.id">
          <td><img :src="contact.pictureUrl"></td>
          <td>{{ contact.name }}</td>
          <td>{{ contact.popularity.toFixed(2) }}</td>
          <td v-if="contact.wonOscar">🏆</td> <!--Iteration 3 display Awards Info-->
          <td v-else></td>
          <td v-if="contact.wonEmmy">🏆</td>
          <td v-else></td>
          <td><button @click="removeContacts(contact.id)">Delete</button></td> <!--Iteration 5: Delete button-->
        </tr>
      </tbody>
    </table>

  </div>
</template>

<!--<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <HelloWorld msg="Hello Vue 3 + Vite" />
</template>-->

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1 {
 text-align: center;
 font-size: 10 rem;
 font-weight: bold;
 background-color: blue;
 color: aliceblue;
 
}
.title {
  text-align: center;
  font-size: 10 rem;
  font-weight: 700;  
}

.buttons {
  display: flex;
  justify-content: space-around;
  margin: 30px 10px 30px 10px;
  
}

.tablewithinfo{
  text-align: center;
  width: 90%;
  margin: auto;

}

img {
  width: 80px;
}
</style>
