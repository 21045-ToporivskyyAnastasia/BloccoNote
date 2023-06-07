<!-- Template del componente note-list -->
<template id="note-list-template">
    <div>
      <ul class="note-list">
      <li v-for="note in notes" :key="note.id" class="note-item">
        <h3 class="note-title">{{ note.title }}</h3>
        <p class="note-content">{{ note.content }}</p>
        <p class="note-date">Data: {{ note.date.toLocaleDateString("en-US") }}</p>
        <button class="remove-button" @click="confirmRemove(note.id)">Rimuovi</button>
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
  max-width: 750px;
  color:rgb(0, 0, 0);
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
  width: 750px;
  background-color: rgb(66, 76, 87);
  border-radius: 10px;
  padding: 30px;
  position: relative;
  display: flex;
  flex-direction: column;
}
#addNote {
  border: none;
  padding: 10px;
  width: 70px;
  height: 70px;
  cursor: pointer;
  border-radius: 1000px;
  border-radius: 1000px;
  color: rgb(0, 0, 0);
  font-size: 50px;
  position: fixed;
  right: 80px;
  bottom: 80px;
  background-color: rgb(27, 157, 217);
}
</style>