<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
  import contacts from './contacts.json';
  import { reactive } from 'vue';

  const ironContacts = reactive(contacts.splice(0,5));

  function addContact() {
    const position = Math.floor(Math.random()*contacts.length);
    const removeRandomContact = contacts.splice(position, 1);
    const randomContact = removeRandomContact.pop();

    ironContacts.push(randomContact);
  };

  function removeContact(id) {
    ironContacts.forEach((contact, index) => {
      if (contact.id === id) {
        ironContacts.splice(index, 1);
        contacts.push(contact);
      };
    });
  };

  function sortByName(a,b) {
    if (a.name < b.name) {return -1};
    if (a.name> b.name) {return 1};
    return 0;
  };

  function sortByPopularity(a,b) {
    if (a.popularity < b.popularity) {return 1};
    if (a.popularity> b.popularity) {return -1};
    return 0;
  };

  function sortIronContactsByName(){
    ironContacts.sort(sortByName);
  };

  function sortIronContactsByPopularity(){
    ironContacts.sort(sortByPopularity);
  };
</script>

<template>
  <h1>IronContacts</h1>
  <div class="buttons">
    <button @click="addContact" type="button" id="addButton">Add Random Contact</button>
    <button @click="sortIronContactsByPopularity" type="button" class="sortedButtons">Sort by popularity</button>
    <button @click="sortIronContactsByName" type="button" class="sortedButtons">Sort by name</button>
  </div>
  <table>
    <thead>
      <tr>
        <th>Picture</th>
        <th>Name</th>
        <th>Popularity</th>
        <th>Won an Oscar</th>
        <th>Won an Emmy</th>
        <th>Actions</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="contact in ironContacts" :key="contact.id">
        <td> <img :src="contact.pictureUrl" /></td>
        <td> {{ contact.name }} </td>
        <td> {{ contact.popularity.toFixed(2) }} </td>
        <td>
          <span v-show="contact.wonOscar">
            <img src="./img/oscar.png" class="premio"/>
          </span>
        </td>
        <td> 
          <span v-show="contact.wonEmmy">
            <img src="./img/emmy.png" class="premio"/>
          </span>
        </td>
        <td>
          <button @click="removeContact(contact.id)" type="button" class="removeButtons">Delate</button>
        </td>
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

  table {
    margin: auto;
  }

  img {
    width: 70px;
    height: auto;
  }

  .premio {
    width: 30px;
    height: auto;
  }

  .buttons {
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    max-width: 50%;
    margin: 1rem auto;
  }
  button {
    border: none;
    border-radius: 10px;
    padding: 0.6rem;
    cursor: pointer;
    font-weight: bold;
    color: white;
    transition: background-color 1s;
  }
  #addButton {
    background-color: #57cc99;
  }
  #addButton:hover {
    background-color: #80ed99;
  }
  .sortedButtons {
    background-color: #0077b6;
  }
  .sortedButtons:hover {
    background-color: #00b4d8;
  }
  .removeButtons {
    background-color: #f08080;
  }
  .removeButtons:hover {
    background-color: #f4978e;
  }
  thead {
    font-size: 1.2rem;
  }
  th,td {
    padding: 1rem;
  }
</style>
