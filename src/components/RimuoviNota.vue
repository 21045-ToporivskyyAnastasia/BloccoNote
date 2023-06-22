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
    props: ["nota"],
    methods: {
      remove() {
        // Logica per rimuovere una nota
        this.$emit('remove-note', this.nota);
      },
      cancel() {
        // Logica per annullare la rimozione di una nota
        this.$emit('cancel');
      }
    }
  }
</script>

<style scoped>  
  * {
    color: black;
  }
  #confirmButton {
    border: 1px solid rgb(66, 76, 87);
    background-color: rgb(27, 157, 217);
    cursor: pointer;
    width: 48%;
    height: 40px;
    color: black;
    font-size: 18px;
    margin-right: 4%;
  }
  #cancelButton {
    border: 1px solid rgb(66, 76, 87);
    background-color: rgb(217, 217, 217);
    cursor: pointer;
    height: 40px;
    width: 48%;
    color: black;
    font-size: 18px;
    transition: background-color 0.3s;
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
    top: 50%;
    left: 50%;
    width: 480px;
    background-color: rgb(66, 76, 87);
    padding: 10px;
    flex-direction: column;
    transform: translate(-50%, -50%);
    display: flex;
    align-items: center;
    margin-top: 3%;
  }
</style>