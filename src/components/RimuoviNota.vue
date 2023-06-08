<!-- Template del componente confirm-remove-modal -->
<template id="confirm-remove-modal-template">
    <div class="modal">
      <div class="modal-content">
        <h2>Conferma Rimozione</h2>
        <p>Sei sicuro di voler rimuovere la nota?</p>
        <div class="modal-buttons">
          <button id="confirmButton" @click="remove">Conferma</button>
          <button id="cancelButton" @click="cancel">Annulla</button>
        </div>
      </div>
    </div>
  </template>

  <script>
    export default{
    name: "RimuoviNota",

    methods: {
        remove() {
          // Logica per rimuovere una nota
          this.$emit('remove-note');
        },
        cancel() {
          // Logica per annullare la rimozione di una nota
          this.$emit('cancel');
        },

      },
  }

</script>
<style scoped>  

  * {
    color: black;
  }
  #confirmButton {
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
  h2 {
    font-weight: bold;
    font-size: 30px;
    color: white;
    text-align: center;
  }
  p {
    font-weight: bold;
    font-size: 20px;
    color: white;
    text-align: center;
    margin-bottom: 20px;
  }
  .modal {
    position: fixed;
    top: 300px;
    left: 150px;
    width: 480px;
    background-color: rgb(66, 76, 87);
    border-radius: 10px;
    padding: 10px;
    flex-direction: column;
  }
</style>