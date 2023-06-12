<!-- Template del componente create-note-modal -->
<template id="create-note-modal-template">
    <div class="modal">
      <div class="modal-content">
        <form @submit.prevent="onSubmit" class="form-group">
          <textarea id="newTitle" v-model="newTitle" placeholder="Inserisci titolo"></textarea>
          <br>
          <textarea id="newContent" v-model="newContent" placeholder="Inserisci testo"></textarea>
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
  export default{
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
  textarea {
    font-size: 24px;
  }
  #newContent {
    height: 350px;
    width: 605px;
    background-color: rgb(66, 76, 87);
    color: white;
  }
  #newTitle {
    height: 50px;
    width: 605px;
    background-color: rgb(66, 76, 87);
    color: white;
  }
  .modal {
    width: 650px;
    background-color: rgb(66, 76, 87);
    border-radius: 10px;
    padding: 30px;
    position: fixed;
    top: 150px;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-left: 50px;
  }
  .modal-buttons {
    padding: 10px 20px;
    font-size: 30px;
    width: 100%;
    color: white;
    margin-top: 10px;
  }
  #submitButton {
    border: 1px solid rgb(66, 76, 87);
    border-radius: 15px;
    background-color: rgb(27, 157, 217);
    cursor: pointer;
    width: 50%;
    height: 40px;
    width: 50%;
    color: black;
    font-size: 18px;
  }
  #cancelButton {
    border: 1px solid rgb(66, 76, 87);
    border-radius: 15px;
    background-color: rgb(217, 217, 217);
    cursor: pointer;
    height: 40px;
    width: 50%;
    color: black;
    font-size: 18px;
  }
</style>