<!-- Template del componente note-list -->
<template id="note-list-template">
    <div id="container">
      <ul class="note-list">
      <li v-for="note in notes" :key="note.id" class="note-item">
        <button class="remove-button" @click="confirmRemove(note)">x</button>
        <h3 class="note-title">
          {{ note.title }}
        </h3>
        <p class="note-content">{{ note.content }}
          <button class="expand-button" @click="">↓</button>
        </p>
        <p class="note-date">Data: {{ note.date }}
          <button class="edit-button" @click="showModificaNota(note)">Modifica</button>
        </p>

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
        //Logica per modificare una nota schiacciando il pulsante "modifica"
        showModificaNota(note){
            this.$emit('modifica-nota', note)
          },
        //Logica per modificare una nota schiacciando il pulsante "+"
        showAddNote(){
          this.$emit('add-note');
        },
        //Logica per fare uscire il pop-up di conferma rimozione schiacciando il tasto "x"
        confirmRemove(id) {
          this.$emit('confirm-remove', id);
        },
      },
  }
  </script>
  <!--design della schermata principale con tutte le note con css-->
<style scoped>
  * {
    color: black;
  }
  #container {
    justify-content: center;  
  }
  .note-list {
    margin-top: 0;
    background-color: white;
    padding-top: 150px;
    padding-left: 0; 
    justify-content: center;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .edit-button{
    background-color: rgb(27, 157, 217);
    border: none;
    padding-bottom: 2px;
    font-size: 15px;
    position: absolute; 
    right: 9.1%;
    width: 80px;
    position: flex;
  }
  .expand-button {
    background-color: rgb(217, 217, 217);
    border: none;
    font-size: 20px;
    position: absolute; 
    right: 9.3%;
    position: flex;
    color: rgb(27, 157, 217);
    font-weight: bolder;
  }
  .remove-button {
    background-color: rgb(27, 157, 217);
    height: 40px;
    width: 40px;
    border: none;
    font-size: 20px;
    position: absolute;
    right: 9.2%;
  }
  .note-item {
    width: 82%;
    height: auto;
    background-color: rgb(217, 217, 217);
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-bottom: 30px;
    border: 1px solid rgb(66, 76, 87);
  }
  h3 {
    font-size: 24px;
    font-weight: bold;
    margin-bottom: 5px;
    padding-bottom: 2px;
    word-wrap: break-word;
    background-color: rgb(66, 76, 87);
    color: white;
    width: 100%;
    text-align: center;
    justify-content: space-between;
    padding-right: 45px;
  }
  .note-content {
    font-size: 16px;
    white-space: pre-wrap;
    word-wrap: break-word;
    padding-left: 2%;
    padding-right: 2%;
  }
  .note-date {
    font-size: 12.5px;
    margin-top: 8px;
    font-weight: bold;
    padding-left: 2%;
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