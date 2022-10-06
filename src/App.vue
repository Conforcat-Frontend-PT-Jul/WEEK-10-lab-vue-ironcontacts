<template>
  <div class="app">
  </div>
  <div>
    <h1>IronContacts</h1>
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

        <td></td>
      </tr>
  </table>
</div>


</template>

<script setup>
  import contacts from './contacts.json'
  import { ref } from 'vue';

  const fiveContacts = ref(contacts.slice(0, 20)) 

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

</style>