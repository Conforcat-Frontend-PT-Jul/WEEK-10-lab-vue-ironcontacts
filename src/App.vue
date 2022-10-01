<script setup>
import contacts from './contacts'
import { ref } from 'vue'

const contactsToDisplay = ref(contacts.splice(0, 5))
const toggleSortName = ref(true)
const toggleSortPopularity = ref(true)
const isNameSelected = ref(false)
const isPopularitySelected = ref(false)

function randomIntFromInterval(min, max) {
  return Math.floor(Math.random() * (max - min + 1) + min)
}

function addRandomContact() {
  isNameSelected.value = false
  isPopularitySelected.value = false
  const contactNum = randomIntFromInterval(0, contacts.length - 1)
  contactsToDisplay.value.unshift(contacts.splice(contactNum, 1)[0])
}

function removeContact(id) {
  contactsToDisplay.value.forEach((el, index) => {
    if (el.id === id) {
      contactsToDisplay.value.splice(index, 1)[0]
      contacts.push(el)
    }
  })
}

function sortByName(type) {
  toggleSortName.value = !toggleSortName.value
  isNameSelected.value = true
  isPopularitySelected.value = false

  contactsToDisplay.value.sort((a, b) => {
    if (type === 'asc') {
      if (a.name > b.name) return 1
      if (a.name < b.name) return -1
    } else {
      if (a.name < b.name) return 1
      if (a.name > b.name) return -1
    }
    return 0
  })
}
  
function sortByPopularity(type) {
  toggleSortPopularity.value = !toggleSortPopularity.value
  isNameSelected.value = false
  isPopularitySelected.value = true

  contactsToDisplay.value.sort((a, b) => {
    if (type === 'asc') {
      if (a.popularity > b.popularity) return 1
      if (a.popularity < b.popularity) return -1
    } else {
      if (a.popularity < b.popularity) return 1
      if (a.popularity > b.popularity) return -1
    }
    return 0
  })
}
</script>

<template>
  <h2>IronContacts</h2>
  <div class="top-buttons">
    <button @click="addRandomContact">Add random contact</button>
    <span>
      <button v-show="toggleSortName" @click="sortByName('asc')">Sort by name Asc</button>
      <button v-show="!toggleSortName" @click="sortByName('des')">Sort by name Des</button>
    </span>
    <span>
      <button v-show="toggleSortPopularity" @click="sortByPopularity('asc')">Sort by popularity Asc</button>
      <button v-show="!toggleSortPopularity" @click="sortByPopularity('des')">Sort by popularity Des</button>
    </span>
  </div>
  <table>
    <thead>
      <tr>
        <th>Picture</th>
        <th class="sortable" :class="{selected: isNameSelected, revert: toggleSortName}">Name</th>
        <th class="sortable" :class="{selected: isPopularitySelected, revert: toggleSortPopularity}">Popularity</th>
        <th>Won Oscar</th>
        <th>Won Emmy</th>
        <th>Actions</th>
      </tr>
    </thead>
    <tbody>
      <TransitionGroup name="list">
        <tr
          v-for="contact in contactsToDisplay"
          :key="contact.id"
        >
          <td><img :src="contact.pictureUrl" /></td>
          <td>{{ contact.name }}</td>
          <td>{{ contact.popularity.toFixed(2) }}</td>
          <td>
            <span v-if="contact.wonOscar">🏆</span>
          </td>
          <td>
            <span v-if="contact.wonEmmy">🏆</span>
          </td>
          <td>
            <button @click="removeContact(contact.id)" class="remove">Delete</button>
          </td>
        </tr>
      </TransitionGroup>
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
.top-buttons button {
  margin: 0 20px 20px;
}
button {
  display: inline-block;
  font-weight: 400;
  text-align: center;
  white-space: nowrap;
  vertical-align: middle;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  border: 1px solid transparent;
  padding: 0.375rem 0.75rem;
  font-size: 1rem;
  line-height: 1.5;
  border-radius: 0.25rem;
}
button:hover {
  cursor: pointer;
  opacity: .8;
  transition: all .3s ease-in-out;
}
.remove {
  color: #fff;
  background-color: #dc3545;
  border-color: #dc3545;
}
table {
  margin: 0 auto;
}
th, td {
  padding: 10px 20px;
}
.selected.sortable:after {
  content: '>';
  display: inline-block;
  width: 15px;
  height: 15px;
  transform: rotate(90deg);
  color: #c2c2c2;
  text-align: center;
  line-height: 15px;
  margin-left: 5px;
}
.selected.sortable.revert:after {
  transform: rotate(-90deg);
}
img {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  object-fit: cover;
}
.selected {
  background: #282828;
  color: white;
  border-radius: 25px;
}
.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
</style>
