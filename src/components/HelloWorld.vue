<template>
<h1>IronContacts</h1>
<button @click="addRandomContact">Add Random Contact</button>
<button @click="sortByName">Sort by Name</button>
<button @click="sortByPopularity">Sort by Popularity </button>
<div class="tableStyle">
<table>
  <thead>
    <tr>
      <th><h3>Picture</h3></th>
      <th><h3>Name</h3></th>
      <th><h3>Popularity</h3></th>
      <th><h3>Oscar</h3></th>
      <th><h3>Emmy</h3></th>
      <th><h3>Delete</h3></th>
    </tr>
  </thead>
 <tbody>
    <tr v-for="contact in displayContacts" :key="contact.id">
        <td><img class="imageSize" v-bind:src="contact.pictureUrl"></td>
        <td>{{contact.name}}</td>
        <td>{{(contact.popularity).toFixed(2)}}</td>
        <td>{{contact.wonOscar ? "🏆":""}}</td>
        <td>{{contact.wonEmmy ? "🏆":""}}</td>
        <td><button @click="deleteContact (contact.id)">Delete</button></td>
      </tr>
    </tbody>
</table>
</div>
</template>

<script setup>
import {reactive} from 'vue'
import contacts from "../contacts.json"

  const myContacts = reactive (contacts);
  //console.log(myContacts);
  let displayContacts = reactive (contacts.slice(0, 5))


function addRandomContact(){
       if(contacts.length>0){
      let newContact = contacts.splice(Math.floor(Math.random()*contacts.length-1),1);
  displayContacts.push(newContact[0]);
  }
} 

function sortByName(){
    displayContacts.sort(function (a, b) {
  if (a.name > b.name) {
    return 1;
  }
  if (a.name < b.name) {
    return -1;
  }
  return 0;
})
}
function sortByPopularity(){
displayContacts.sort(function (a, b) {
  if (a.popularity > b.popularity) {
    return -1;
  }
  if (a.popularity < b.popularity) {
    return 1;
  }
  return 0;
})
}
function deleteContact(id){
  let index = displayContacts.findIndex(contact => contact.id == id);
  contacts.push(...displayContacts.splice(index,1))
}


</script>

<style>
.imageSize {
  width: 50px;
}
.tableStyle {
  display: flex;
  justify-content: center;
}
</style>