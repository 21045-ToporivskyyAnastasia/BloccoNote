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
  max-width: 750px;
  color:rgb(0, 0, 0);
}
main {
    margin: 0 auto;
    width: 750px;
    background-color: white;
}
.note-list {
  max-width: 1000px;
  margin-top: 150px;
  background-color: white;
}
h1 {
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 75px;
  color: white;
  margin-left: 20px;
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
  align-items: left;
}
.note-content {
  font-size: 16px;
}
h3 {
  font-size: 24px;
  font-weight: bold;
  margin-bottom: 10px;
}
.note-date {
  font-size: 12.5px;
  margin-top: auto;
  font-weight: bold;
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
  padding: 12px;
  width: 80px;
  height: 80px;
  cursor: pointer;
  border-radius: 1000px;
  color: rgb(0, 0, 0);
  font-size: 50px;
  position: absolute;
  right: 60px;
  bottom: 60px;
  background-color: rgb(27, 157, 217);
}
</style>