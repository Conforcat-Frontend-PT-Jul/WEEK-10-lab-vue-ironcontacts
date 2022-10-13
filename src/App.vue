<script>
import { ref } from "vue";
import contacts from "./contacts.json";
const contactsArr = ref(contacts);
const firstFive = ref(contactsArr.value.slice(0, 5));
const byNameBool = ref(false);
const byPopularityBool = ref(false);
const addRandom = () => {
  const randomizer = Math.floor(Math.random() * contactsArr.value.length);
  const randomContact = contactsArr.value[randomizer];
  if (firstFive.value.includes(randomContact)) {
    addRandom();
  } else {
    firstFive.value.push(randomContact);
  }
  contactsArr.value.splice(randomizer, 1);
  return firstFive.value;
};
const sortbyNameBool = () => {
  byNameBool.value = true;
  byPopularityBool.value = false;
  return firstFive.value.sort((a, b) => {
    if (a.name < b.name) {
      return -1;
    }
    if (a.name > b.name) {
      return 1;
    }
    return 0;
  });
};
const sortbyPopularityBool = () => {
  byNameBool.value = false;
  byPopularityBool.value = true;
  return firstFive.value.sort((a, b) => {
    return b.popularity - a.popularity;
  });
};
const deleteContact = (index) => {
  contactsArr.value.push(firstFive.value[index]);
  return firstFive.value.splice(index, 1);
};
export default {
  name: "TheIronContacts",
  setup() {
    return {
      contactsArr,
      firstFive,
      addRandom,
      sortbyNameBool,
      sortbyPopularityBool,
      deleteContact,
      byNameBool,
      byPopularityBool,
    };
  },
};
</script>
<template>
  <h1>IRONCONTACTS</h1>
  <div>
    <button @click="addRandom" id="add_random_button">
      Add Random Contact
    </button>
    <button @click="sortbyNameBool">Sort by Name</button>
    <button @click="sortbyPopularityBool">Sort by Popularity</button>
    <br />
    <br />
  </div>
  <div class="table">
    <table>
      <thead>
        <tr>
          <th>Picture</th>
          <th>Name</th>
          <th>Popularity</th>
          <th>Oscar winner</th>
          <th>Emmy winner</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="contact in firstFive" :key="contact.id">
          <td>
            <img :src="contact.pictureUrl" alt="contact" />
          </td>
          <td>{{ contact.name }}</td>
          <td>{{ contact.popularity.toFixed(2) }}</td>
          <td>{{ contact.wonOscar ? "🏆" : "" }}</td>
          <td>{{ contact.wonEmmy ? "🌟" : "" }}</td>
          <td>
            <button @click="deleteContact(index)" id="delete_button">
              Delete
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<style>
@import url("https://fonts.googleapis.com/css?family=Roboto:100,300,400,500,700&display=swap");
#app {
  font-family: Roboto;
  text-align: center;
  margin-top: 10vh;
}
html {
  scroll-behavior: smooth;
}
h1 {
  font-size: 60px;
  font-weight: 500;
}
button {
  background-color: lightskyblue;
  border: none;
  border-radius: 12px;
  padding: 10px 10px;
  text-align: center;
  font-size: 16px;
  margin: 4px 8px;
  cursor: pointer;
}
#add_random_button {
  background-color: lightgreen;
}
#delete_button {
  background-color: lightcoral;
}
.table {
  display: flex;
  justify-content: center;
  width: 100%;
  max-width: 60%;
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
}
</style>
