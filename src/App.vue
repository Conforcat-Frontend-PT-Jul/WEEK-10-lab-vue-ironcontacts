<script>
import { ref, computed } from "vue";
import contacts from "./contacts.json";

const contactsList = ref(contacts);

const fiveContacts = computed(() => {
  return contactsList.value.slice(0, 5);
});

const addRandomContact = () => {
  const randomIndex = Math.floor(Math.random() * contactsList.value.length);
  const randomContact = contactsList.value[randomIndex];

  if (fiveContacts.value.includes(randomContact)) {
    addRandomContact();
  } else {
    fiveContacts.value.push(randomContact);
  }

  fiveContacts.value.push(contactsList.value[randomIndex]);

  contactsList.value.splice(randomIndex, 1);

  return fiveContacts.value;
};

export default {
  name: "TheIronContacts",
  setup() {
    return {
      contactsList,
      fiveContacts,
      addRandomContact,
    };
  },
};
</script>

<template>
  <h1>IronContacts</h1>
  <div>
    <button @click="addRandomContact">Add Random Contact</button>
    <button>Sort by Name</button>
    <button>Sort by Popularity</button>
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
