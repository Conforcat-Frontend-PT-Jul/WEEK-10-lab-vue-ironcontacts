<script setup>
import contacts from "./contacts.json";
import { ref, reactive } from "vue";
const firstFiveContacts = reactive(contacts.slice(0, 5));
const otherContacts = reactive(contacts.slice(5));
const contactsList = firstFiveContacts;


const addRandomContact = () => {
  const randomContact = otherContacts[Math.floor(Math.random() * otherContacts.length)];
  contactsList.push(randomContact);
};
const sortByName = () => {
  contactsList.sort(function (a, b) {
    if (a.name < b.name) {
      return -1;
    }
    if (a.name > b.name) {
      return 1;
    }
    return 0;
  });
};

const sortByPopularity = () => {
  contactsList.sort(function (a, b) {
    if (a.popularity < b.popularity) {
      return 1;
    }
    if (a.popularity > b.popularity) {
      return -1;
    }
    return 0;
  });
};

const deleteContact = (el) => {
  const index = contactsList.findIndex((contact) => {
    return contact.id === el;
  });
  contactsList.splice(index, 1);
};
</script>

<template>
  <div class="container shadow-sm p-3 mb-5 bg-body rounded">
    
    <nav class="navbar navbar-expand-lg bg-light">
      <div class="container-fluid">
        <span class="navbar-brand"><h2> Iron Contacts</h2></span>
      </div>
      <form class="container-fluid justify-content-start">
        <button class="btn btn-outline-success me-2" type="button" @click="addRandomContact">Add Random Contact</button>
        <button class="btn btn-outline-success me-2" type="button" @click="sortByName">Sort by name</button>
        <button class="btn btn-outline-success me-2" type="button" @click="sortByPopularity">Sort by popularuty</button>
      </form>
    </nav>
    <table class="table table-striped">
      <tr>
        <th class="col-sm-2 text-center">Picture</th>
        <th class="col-sm-3 text-center">Name</th>
        <th class="col-sm-2 text-center">Popularity</th>
        <th class="col-sm-2 text-center">Won an Oscar</th>
        <th class="col-sm-2 text-center">Won an Emmy</th>
      </tr>
      <tr class="position-relative" v-for="contact in contactsList" :key="contact.id">
        <td class="text-center">
          <img class="img-thumbnail" style="width: 120px" :src="contact.pictureUrl" alt="foto" />
        </td>
        <td class="text-center">{{ contact.name }}</td>
        <td class="text-center">{{ contact.popularity.toFixed(2) }}</td>
        <td v-if="contact.wonOscar" class="text-center">🏆</td>
        <td v-else></td>
        <td v-if="contact.wonEmmy" class="text-center">🏆</td>
        <td v-else></td>
        <button
        type="button"
        class="btn btn-danger btn-sm position-absolute top-50 end-0 translate-middle-y"
        @click="deleteContact(contact.id)"
        >
        Delete
      </button>
    </tr>
  </table>
</div>
  
</template>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins&display=swap");
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: Arial, Helvetica, sans-serif;
}

h1 {
  text-align: center;
}
</style>
