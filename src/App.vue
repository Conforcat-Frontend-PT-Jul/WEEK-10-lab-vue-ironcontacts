<template>
  <div class="app">
  </div>
  <header>
    <div class="ironContacts">
    <h1>IronContacts</h1>
    <div>
    <button @click="addRandomContact" >Add Random Contact</button>
    <button @click="sortPopularity" >Sort By Popularity</button>
    <button @click="sortName" >Sort By Name</button>
    </div>
    </div>
  </header>
  <table class="table">
      <tr>
        <th>Picture</th>
        <th>Name</th>
        <th>Popularity</th>
        <th>Won an Oscar</th>
        <th>Won an Emmy</th>
      </tr>
      <tr v-for="contact in fiveContacts">
        <td><img :src="contact.pictureUrl"></td>
        <td>{{ contact.name }}</td>
        <td>{{ contact.popularity.toFixed(2) }}</td>
        <td v-if="contact.wonOscar">🏆</td>
        <td v-else="contact.wonOscar"></td>
        <td v-if="contact.wonEmmy">🏆</td>
        <td v-else="contact.wonEmmy"></td>
        <button @click="deleteContact(contact.id)">Delete</button>
        <td></td>
      </tr>
  </table>



</template>

<script setup>
  import contacts from './contacts.json'
  import { ref } from 'vue';

  const fiveContacts = ref(contacts.slice(0, ));

  function addRandomContact() {
  let randomContact = contacts[Math.floor(Math.random() * contacts.length)];
  if (fiveContacts.value.includes(randomContact)) {
    return;
  } else {
    fiveContacts.value.push(randomContact);
  }
}

  function sortPopularity(){
  fiveContacts.value.sort((a, b) => b.popularity - a.popularity);
  return fiveContacts;

  }

  function sortName(){
   fiveContacts.value.sort((a, b) => a.name.localeCompare(b.name));
  return fiveContacts;
  }

  function deleteContact(id) {
  fiveContacts.value.forEach((contact, index) => {
       if (contact.id === id) {
      fiveContacts.value.splice(index, 1);
     
      return fiveContacts;
    }
  });
}

</script>

<style>

h1 {
  text-align: center;
}

img {
  width: 80px;
}

.table {
  text-align: center;
  margin: 30px auto 30px auto;

}
.ironContacts {
text-align: center;

}
</style>