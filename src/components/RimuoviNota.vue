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
  max-width: 750px;
  color:rgb(0, 0, 0);
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
.newContent {
  height: 300px;
  width: 690px;
  background-color: rgb(66, 76, 87);
  color: white;
}
.newTitle {
  height: 50px;
  width: 690px;
  background-color: rgb(66, 76, 87);
  color: white;
}
main {
    margin: 0 auto;
    width: 750px;
    background-color: white;
}
.container {
  max-width: 1000px;
  margin: 0 auto;
  background-color: white;
}
h1 {
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 75px;
  color: white;
  margin-left: 20px;
}
.card {
  width: 600px;
  height: 175px;
  background-color: rgb(217, 217, 217);
  padding: 10px;
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-left: 70px;
  margin-top: 30px;
  align-items: left;
}
.note-content {
  line-height: 1.25;
  font-size: 14px;
}
.note-title {
  font-size: 20px;
  font-weight: bold;
  margin-bottom: 10px;
}
.note-date {
  font-size: 12.5px;
  margin-top: auto;
}
header {
  display: flex;
  width: 750px;
  align-items: center;
  justify-content: space-between;
  background-color: rgb(66, 76, 87);
}
.cards-container {
  display: flex;
  flex-wrap: wrap;
}
.overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.77);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 10;
}
main {
  height: 100vh;
  width: 100vw;
}
.modal {
  width: 650px;
  background-color: rgb(66, 76, 87);
  border-radius: 10px;
  padding: 30px;
  position: relative;
  display: flex;
  flex-direction: column;
}
.modal p {
  margin-left: auto;
  font-size: 20px;
  z-index: 100000;
  cursor: pointer;
}
textarea {
  width: 100%;
  height: 200px;
  padding: 5px;
  font-size: 20px;
}
.showAddNote {
  border: none;
  padding: 10px;
  margin-right: 20px;
  width: 70px;
  height: 70px;
  cursor: pointer;
  background-color: rgb(27, 157, 217);
  border-radius: 1000px;
  color: rgb(0, 0, 0);
  font-size: 50px;
}
</style>