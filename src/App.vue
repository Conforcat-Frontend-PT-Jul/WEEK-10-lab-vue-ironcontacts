<script setup>
import contacts from "./contacts.json";
import { ref, reactive } from "vue";
const firstFiveContacts = reactive(contacts.slice(0, 5));
const contactsList = firstFiveContacts;
const addRandomContact = () => {
  const randomContact = contacts[Math.floor(Math.random() * contacts.length)];
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
  <div class="contact-card">
    <h1>Iron Contacts</h1>
    {{ randomContact }}
    <div menu-btn>
      <button class="btn" @click="addRandomContact">Add Random Contact</button>
      <button class="btn" @click="sortByName">Sort by name</button>
      <button class="btn" @click="sortByPopularity">Sort by popularuty</button>
    </div>
    <table>
      <tr>
        <th>Picture</th>
        <th>Name</th>
        <th>Popularity</th>
        <th>Won an Oscar</th>
        <th>Won an Emmy</th>
      </tr>
      <tr v-for="contact in contactsList" :key="contact.id">
        <td>
          <img class="contact-image" :src="contact.pictureUrl" alt="foto" />
        </td>
        <td>{{ contact.name }}</td>
        <td>{{ contact.popularity.toFixed(2) }}</td>
        <td v-if="contact.wonOscar">🏆</td>
        <td v-else></td>
        <td v-if="contact.wonEmmy">🏆</td>
        <td v-else></td>
        <button @click="deleteContact(contact.id)">Delete</button>
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

.contact-image {
  width: 70px;
}

.contact-card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  width: 80%;
  margin: 3em auto;
  padding: 3em;
}
table {
  table-layout: auto;
  width: 100%;
}
</style>
