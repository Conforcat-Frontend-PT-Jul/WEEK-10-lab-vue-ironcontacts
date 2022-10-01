<script>
import contacts from "./contacts.json";
import { ref, computed } from "vue";

const contactsList = ref(contacts);
const fiveContacts = computed(() => {
  return contactsList.value.slice(0, 5);
});

export default {
  name: "TheIronContacts",
  setup() {
    return {
      contactsList,
      fiveContacts,
    };
  },
};
</script>

<template>
  <h1>IronContacts</h1>
  <div>
    <button>Add Random Contact</button>
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
        </tr>
      </thead>
      <tbody>
        <tr v-for="contact in fiveContacts" :key="contact.id">
          <td>
            <img :src="contact.pictureUrl" alt="contact" />
          </td>
          <td>{{ contact.name }}</td>
          <td>{{ contact.popularity.toFixed(2) }}</td>
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
