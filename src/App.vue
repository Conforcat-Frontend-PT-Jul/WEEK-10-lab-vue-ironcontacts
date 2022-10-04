<script>
import { ref } from "vue";
import contacts from "./contacts.json";

const contactsList = ref(contacts);
const fiveContacts = ref(contactsList.value.slice(0, 5));
const byName = ref(false);
const byPopularity = ref(false);

const addRandomContact = () => {
  const randomIndex = Math.floor(Math.random() * contactsList.value.length);
  const randomContact = contactsList.value[randomIndex];

  if (fiveContacts.value.includes(randomContact)) {
    addRandomContact();
  } else {
    fiveContacts.value.push(randomContact);
  }

  contactsList.value.splice(randomIndex, 1);

  return fiveContacts.value;
};

const sortByName = () => {
  byName.value = true;
  byPopularity.value = false;
  return fiveContacts.value.sort((a, b) => {
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
  byName.value = false;
  byPopularity.value = true;
  return fiveContacts.value.sort((a, b) => {
    return b.popularity - a.popularity;
  });
};

export default {
  name: "TheIronContacts",
  setup() {
    return {
      contactsList,
      fiveContacts,
      addRandomContact,
      sortByName,
      sortByPopularity,
      byName,
      byPopularity,
    };
  },
};
</script>

<template>
  <h1>IronContacts</h1>
  <div>
    <button @click="addRandomContact">Add Random Contact</button>
    <button @click="sortByName">Sort by Name</button>
    <button @click="sortByPopularity">Sort by Popularity</button>
  </div>

  <div class="table">
    <table>
      <thead>
        <tr>
          <th>Picture</th>
          <th>Name</th>
          <th>Popularity</th>
          <th>Won Oscar</th>
          <th>Won Emmy</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="contact in fiveContacts" :key="contact.id">
          <td>
            <img :src="contact.pictureUrl" alt="contact" />
          </td>
          <td>{{ contact.name }}</td>
          <td>{{ contact.popularity.toFixed(2) }}</td>
          <td>{{ contact.wonOscar ? "🏆" : "No" }}</td>
          <td>{{ contact.wonEmmy ? "🏆" : "No" }}</td>
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

h1 {
  font-size: 40px;
  font-weight: 100;
}

.table {
  display: flex;
  justify-content: center;
  width: 100%;
  max-width: 1280px;
  margin: 0 auto;
}

img {
  width: 100px;
}

table {
  width: 100%;
  border-collapse: collapse;
}

th,
td {
  padding: 15px;
  text-align: left;
  border-bottom: 1px solid #ddd;
}

tr:hover {
  background-color: #f5f5f5;
}

button {
  background-color: #4caf50;
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
}

button:hover {
  background-color: #45a049;
}
</style>
