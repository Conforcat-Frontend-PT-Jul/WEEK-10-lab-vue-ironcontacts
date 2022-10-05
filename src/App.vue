<script setup>
import allContacts from './contacts.json'
import { ref } from 'vue';

const contacts = ref([]);
const remainingContacts = ref([]);
remainingContacts.value = [...allContacts];

for(let i=0; i<5; i++) {
  contacts.value.push(allContacts[i]); 
  remainingContacts.value.shift();
}

console.log(contacts.value)
  console.log(remainingContacts.value)

function addRandomContact() {
  const randomItem = Math.floor(Math.random() * remainingContacts.value.length) ;
  console.log(contacts.value.length, remainingContacts.value.length, randomItem)
  contacts.value.push(remainingContacts.value[randomItem]);
  remainingContacts.value = remainingContacts.value.filter((_, i) => i !== randomItem);
  console.log(contacts.value)
  console.log(remainingContacts.value)
}

function addRandomContact2() {
  //const randomItem = Math.floor(Math.random() * remainingContacts.value.length) ;
 
  //contacts.value.splice(3,2)
  contacts.value.push(remainingContacts.value[3]);
  remainingContacts.value = remainingContacts.value.filter((_, i) => i !== 3)
  console.log(contacts.value)
  console.log(remainingContacts.value)
  //console.log(newArr.value)
  //contacts.value.push(remainingContacts.value[randomItem]);
  //remainingContacts.value.splice(randomItem,1)
}

function sortContacts(attr) {
  if(attr === 'Popularity') {
    contacts.value.sort( (a,b) => b.popularity - a.popularity )
  } else if (attr === 'Name') {
    contacts.value.sort( (x,y) => {  
          let a = x.name.toUpperCase(),
              b = y.name.toUpperCase();
          return a == b ? 0 : a > b ? 1 : -1; 
    })
  }
}

</script>

<template>
  <header>
    <h1>IronContacts</h1>
  </header>
  <div>
    <button @click="addRandomContact">Add random contact</button>
    <button @click="sortContacts('Popularity')">Sort by popularity</button>
    <button @click="sortContacts('Name')">Sort by name</button>
  </div>
  <br>
  <table>
    <tr>
      <th>Picture</th>
      <th>Name</th>
      <th>Popularity</th>
      <th>Won an Oscar</th>
      <th>Won an Emmy</th>
      <th>Actions</th>
    </tr>
    <tr v-for="contact in contacts" :key="contacts.name">
      <td>
        <img alt="Celebrity picture" :src=contact.pictureUrl>
      </td>
      <td> {{ contact.name }} </td>
      <td> {{ contact.popularity }} </td>
      <td v-if="contact.wonOscar">
        <img class="trophy" alt="trophy image" src="./assets/images/trophy.png">
      </td>
      <td v-if="contact.wonEmmy">
        <img class="trophy" alt="trophy image" src="./assets/images/emmy.png">
      </td>
      <td>
        <button @click="removeContact">Delete</button>
      </td>
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

.trophy {
  width: 25px;
}
</style>
