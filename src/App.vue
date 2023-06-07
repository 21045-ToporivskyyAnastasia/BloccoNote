<template>
  <h1>Blocco Note</h1>
  <ListaNote @add-note="showCreateNote=true" @confirm-remove="showRemoveNote=true" :notes="notes" ></ListaNote>
  <RimuoviNota v-if="showRemoveNote" @remove-note="removeNote" @cancel="showRemoveNote=false"/>
  <CreaNota v-if="showCreateNote" @add-note="addNote" @cancel="showCreateNote=false"/>
</template>

<script>
    import CreaNota from "./components/CreaNota.vue";
    import ListaNote from "./components/ListaNote.vue";
    import RimuoviNota from "./components/RimuoviNota.vue";

    export default{
        name: "App",
        components:{ 
          CreaNota,
          ListaNote,
          RimuoviNota,
        },
        data(){
          return {
            showCreateNote:false,
            showRemoveNote:false,
            notes: [],
          }
        },
        methods:{
          removeNote(id){
          this.notes.pop()
          this.showRemoveNote=false;
          },
          addNote(id,title,content,date){
            const note = {
              id: id,
              title: title,
              content: content,
              date: date,
            };

            console.log(note);
            this.notes.push(note.id);
            this.showCreateNote = false;
          }
        }
        
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
.modal-buttons button {
  padding: 10px 20px;
  font-size: 20px;
  width: 50%;
  background-color: rgb(27, 157, 217);
  border: none;
  color: white;
  cursor: pointer;
  margin-top: 15px;
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