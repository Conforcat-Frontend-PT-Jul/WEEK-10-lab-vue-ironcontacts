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

const deleteContact = (index) => {
  contactsList.value.push(fiveContacts.value[index]);
  return fiveContacts.value.splice(index, 1);
};

const reset = () => {
  contactsList.value = contacts;
  fiveContacts.value = contactsList.value.slice(0, 5);
  byName.value = false;
  byPopularity.value = false;
};

const addAllContacts = () => {
  contactsList.value = [];
  return (fiveContacts.value = contacts);
};

const popularity = (popularity) => {
  return popularity.toFixed(2);
};

//if popularity is >= 15 then add a class to the element
const popularityClass = (popularity) => {
  if (popularity >= 15) {
    return "popular";
  }
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
      deleteContact,
      byName,
      byPopularity,
      reset,
      addAllContacts,
      popularity,
      popularityClass,
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
    <button class="reset" @click="reset">Reset</button>
    <button class="info" @click="addAllContacts">Add All Contacts</button>
  </div>

  <div class="table">
    <table class="sort">
      <thead>
        <tr>
          <th>Picture</th>
          <th>Name</th>
          <th>Popularity</th>
          <th>Won Oscar</th>
          <th>Won Emmy</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="contact in fiveContacts"
          :key="contact.id"
          :class="popularityClass(contact.popularity)"
        >
          <td>
            <img :src="contact.pictureUrl" alt="contact" />
          </td>
          <td>{{ contact.name }}</td>
          <td>{{ contact.popularity.toFixed(2) }}</td>
          <td>{{ contact.wonOscar ? "🏆" : "No" }}</td>
          <td>{{ contact.wonEmmy ? "🏆" : "No" }}</td>
          <td>
            <button class="delete" @click="deleteContact(index)">
              Delete 🗑️
            </button>
          </td>
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
  padding: 3rem 0;
}

img {
  border-top-left-radius: 50% 50%;
  border-top-right-radius: 50% 50%;
  border-bottom-right-radius: 50% 50%;
  border-bottom-left-radius: 50% 50%;
  object-fit: cover;
  width: 150px;
  height: 150px;
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
  text-align: center;
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

button:active {
  background-color: #4caf50;
  box-shadow: 0 5px #666;
  transform: translateY(4px);
}

button:focus {
  outline: none;
}

.reset {
  background-color: #f49236;
}

.reset:hover {
  background-color: #f49236;
}

.reset:active {
  background-color: #f49236;
  box-shadow: 0 5px #666;
  transform: translateY(4px);
}

.reset:focus {
  outline: none;
}

.info {
  background-color: #2196f3;
}

.info:hover {
  background-color: #0b7dda;
}

.info:active {
  background-color: #2196f3;
  box-shadow: 0 5px #666;
  transform: translateY(4px);
}

.info:focus {
  outline: none;
}

.delete {
  background-color: #f44336;
}

.delete:hover {
  background-color: #da190b;
}

.delete:active {
  background-color: #f44336;
  box-shadow: 0 5px #666;
  transform: translateY(4px);
}

.delete:focus {
  outline: none;
}

.sort th {
  cursor: pointer;
}

.sort th:hover {
  color: #4caf50;
}

.sort th:active {
  color: #4caf50;
  box-shadow: 0 5px #666;
  transform: translateY(4px);
}

.popular {
  background-color: rgba(255, 217, 0, 0.226);
}
</style>
