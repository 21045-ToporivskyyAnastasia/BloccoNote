<!-- Template del componente create-note-modal -->
<template id="create-note-modal-template">
  <div class="modal">
    <div class="modal-content">
      <form @submit.prevent="onSubmit" class="form-group">
        <textarea id="newTitle" v-model="editedTitle" placeholder="Inserisci titolo" maxlength="100" required></textarea>
        <br>
        <textarea id="newContent" v-model="editedContent" placeholder="Inserisci testo" maxlength="800" required></textarea>
        <br>
        <div class="modal-buttons">
          <button id="submitButton" type="salvaModifica" >Salva</button>
          <button id="cancelButton" @click="cancel" >Annulla</button>
        </div>
      </form>
    </div>
  </div>
</template>


<script>
  export default{
    name: "ModificaNota",
    props:["nota"],
    data() {
        return {
            editedTitle: this.nota.title,
            editedContent: this.nota.content,
            newDate: this.nota.data,
        }
    },
    methods: {
      onSubmit() {
        // Logica per modificare una nota
        this.$emit('modifica-note', {
          id: Date.now(),
          title: this.editedTitle.trim(),
          content: this.editedContent.trim(),
          date: new Date(),
        },
        this.nota
        );
        this.newTitle = '';
        this.newContent = '';
      },
      cancel() {
        // Logica per annullare la modifica di una nota
        this.$emit('cancel');
      }
    }
  }
</script>
<!--design del pop-up modifica nota con css-->
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
    resize: none;
  }
  #newTitle {
    height: 50px;
    width: 605px;
    background-color: rgb(66, 76, 87);
    color: white;
    resize: none;
  }
  .modal {
    width: 650px;
    background-color: rgb(66, 76, 87);
    padding: 30px;
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 3%;
    z-index: 123456789;
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
    background-color: rgb(27, 157, 217);
    cursor: pointer;
    width: 49%;
    height: 40px;
    color: black;
    font-size: 18px;
    margin-right: 2%;
  }
  #cancelButton {
    border: 1px solid rgb(66, 76, 87);
    background-color: rgb(217, 217, 217);
    cursor: pointer;
    height: 40px;
    width: 49%;
    color: black;
    font-size: 18px;
  }
</style>