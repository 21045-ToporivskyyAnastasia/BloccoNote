<!-- Template del componente note-list -->
<template id="note-list-template">
    <div>
      <ul class="note-list">
      <li v-for="note in notes" :key="note.id" class="note-item">
        <h3 class="note-title">{{ note.title }}</h3>
        <p class="note-content">{{ note.content }}</p>
        <p class="note-date">Data: {{ note.date.toLocaleDateString("en-US") }}</p>
        <button class="remove-button" @click="confirmRemove(note.id)">x</button>
      </li>
    </ul>
    <button id="addNote" @click="showAddNote" >+</button>
  </div>
  </template>
  
  <script>
  export default{
    name: "ListaNote",
    props: ['notes'],
    methods: {
      showAddNote(){
        this.$emit('add-note');
      },
          confirmRemove(id) {
            this.$emit('confirm-remove', id);
          },
        },
  }
  </script>
<style scoped>
  * {
    color: black;
  }
  .note-list {
    max-width: 1000px;
    margin-top: 150px;
    background-color: white;
  }
  .remove-button {
    background-color: rgb(27, 157, 217);
    height: 40px;
    width: 40px;
    position: absolute;
    right: 70px;
    border-radius: 4752934756925602579257665629627564765827546276572652485px;
    border: none;
    font-size: 20px;
  }
  .note-item {
    width: 600px;
    height: 175px;
    background-color: rgb(217, 217, 217);
    padding: 10px;
    border-radius: 15px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-top: 30px;
  }
  h3 {
    font-size: 24px;
    font-weight: bold;
    margin-bottom: 10px;
  }
  .note-content {
    font-size: 16px;
  }
  .note-date {
    font-size: 12.5px;
    margin-top: auto;
    font-weight: bold;
  }
  .note-list{
    margin-left: 29px;
  }
  #addNote {
    border: 1.9px solid rgb(0, 0, 0);
    padding: 12px;
    width: 80px;
    height: 80px;
    cursor: pointer;
    border-radius: 391045607px;
    color: rgb(0, 0, 0);
    border-color:black;
    font-size: 50px;
    position: fixed;
    right: 30px;
    bottom: 30px;
    background-color: rgb(27, 157, 217);
  }
</style>