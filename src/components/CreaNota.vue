<!-- Template del componente create-note-modal -->
<template id="create-note-modal-template">
    <div class="modal">
      <div class="modal-content">
        <form @submit.prevent="onSubmit" class="form-group">
          <textarea id="newTitle" v-model="newTitle" placeholder="Inserisci titolo" required></textarea>
          <br>
          <textarea id="newContent" v-model="newContent" placeholder="Inserisci testo" required></textarea>
          <br>
          
          <div class="modal-buttons">
            <button id="submitButton" type="submit" >Salva</button>
            <button id="cancelButton" @click="cancel" >Annulla</button>
          </div>
        </form>
      </div>
    </div>
  </template>

  
  <script>
  export default {
    name: "CreaNota",
    data() {
        return {
          newTitle: '',
          newContent: '',
          newDate: '',
        };
    },
    methods: {
      onSubmit() {
        // Logica per aggiungere una nota
        this.$emit('add-note', {
          id: Date.now(),
          title: this.newTitle.trim(),
          content: this.newContent.trim(),
          date: new Date(),
        });
        this.newTitle = '';
        this.newContent = '';
      },
      cancel() {
        // Logica per annullare la creazione di una nota
        this.$emit('cancel');
      },

    },
  }
  </script>
  <!--design del pop-up crea nota con css-->
  <style scoped>
  * {
    color: black;
  }
  .create-note-modal-template{
    align-items: center;
  }
  textarea {
    font-size: 24px;
  }
  #newContent {
    height: 90%;
    width: 100%;
    background-color: rgb(66, 76, 87);
    color: white;
    resize: none;
  }
  #newTitle {
    min-height: 50px;
    height: 10%;
    width: 100%;
    background-color: rgb(66, 76, 87);
    color: white;
    resize: none;
  }
  .form-group {
    height: 85%;
    width: 100%;
  }
  .modal-content {
    height: 100%;
    width: 100%;
  }
  .modal {
    width: 80%;
    height: 70%;
    background-color: rgb(66, 76, 87);
    padding: 2%;
    position: fixed;
    top: 150px;
    align-items: center;
  }
  .modal-buttons {
    font-size: 30px;
    width: 100%;
    color: white;
  }
  #submitButton {
    border: 1px solid rgb(66, 76, 87);
    background-color: rgb(27, 157, 217);
    cursor: pointer;
    width: 49.5%;
    height: 100%;
    color: black;
    font-size: 18px;
    margin-right: 1%;
  }
  #cancelButton {
    border: 1px solid rgb(66, 76, 87);
    background-color: rgb(217, 217, 217);
    cursor: pointer;
    height: 100%;
    width: 49.5%;
    color: black;
    font-size: 18px;
  }
</style>