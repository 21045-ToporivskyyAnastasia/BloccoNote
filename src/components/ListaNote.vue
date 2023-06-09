<!-- Template del componente note-list -->
<template id="note-list-template">
    <div>
      <ul class="note-list">
      <li v-for="note in notes" :key="note.id" class="note-item">
        <h3 class="note-title">{{ note.title }}</h3>
        <p class="note-content">{{ note.content }}</p>
        <p class="note-date">Data: {{ note.date }}</p>
        <button class="remove-button" @click="confirmRemove(note)">x</button>
        <button class="edit-button" @click="showModificaNota(note)">modifica</button>
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
      showModificaNota(note){
          this.$emit('modifica-nota', note)
        },
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

  .edit-button{
    background-color: rgb(27, 157, 217);
    border: none;
    font-size: 14px;
    position: relative; 
    bottom: 0;
    right: -460px;
    width: 13%;
    border-radius: 10px;
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
    height: auto;
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
    margin-top: 8px;
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
    border-radius: 391045604672569465265475098295863276965709465072965246502965606253046502574857948750284504650647694584909257205627603264954092369024652056039465036757px;
    color: rgb(0, 0, 0);
    border-color:black;
    font-size: 50px;
    position: fixed;
    right: 30px;
    bottom: 30px;
    background-color: rgb(27, 157, 217);
  }
</style>