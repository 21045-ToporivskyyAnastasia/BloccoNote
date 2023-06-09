<template>
  <header>Blocco Note</header>
  <ListaNote @add-note="showCreateNote=true" @modifica-nota="openeditpopup" @confirm-remove="openremovepopup" :notes="notes" ></ListaNote>
  <RimuoviNota v-if="showRemoveNote" :nota="lastclickedNote" @remove-note="removeNote" @cancel="showRemoveNote=false"/>
  <CreaNota v-if="showCreateNote" @add-note="addNote" @cancel="showCreateNote=false"/>
  <ModificaNota v-if="showModificaNote" :nota="lastclickedNote" @modifica-note="modificaNota" @cancel="showModificaNote=false" />
</template>

<script>
  import CreaNota from "./components/CreaNota.vue";
  import ListaNote from "./components/ListaNote.vue";
  import RimuoviNota from "./components/RimuoviNota.vue";
  import ModificaNota from "./components/ModificaNota.vue";

  export default{
      name: "App",
      components:{ 
        CreaNota,
        ListaNote,
        RimuoviNota,
        ModificaNota,
      },
      data(){
        return {
          showModificaNote:false,
          showCreateNote:false,
          showRemoveNote:false,
          notes: [],
          lastclickedNote: null,
        }
      },
      methods:{
        modificaNota(notem,vecchiaNota) {
           const note = {
            id: notem.id,
            title: notem.title,
            content: notem.content,
            date: notem.date,
          };
          this.showModificaNote = false;
          this.notes.push(note);
          const index = this.notes.findIndex(checkid);
          function checkid(noter) {
            return noter.id == vecchiaNota.id;
          }
          this.notes.splice(index, 1);
        },

        removeNote(note){
          const index = this.notes.findIndex(checkid);
          function checkid(noter) {
            return noter.id == note.id;
          }
          this.notes.splice(index, 1);
          this.showRemoveNote=false;
        },
        openremovepopup(note){
          this.lastclickedNote=note;
          this.showRemoveNote=true;
        },
        openeditpopup(note){
          this.lastclickedNote=note;
          this.showModificaNote=true;
        },
        addNote(notem){
          const note = {
            id: notem.id,
            title: notem.title,
            content: notem.content,
            date: notem.date,
          };
          this.notes.push(note);
          this.showCreateNote = false;
          this.showModificaNote=false;
        }
      }
      
    }
</script>
<style>

  #app {
    width: 750px;
    padding: 0;
    margin: 0;
  }
  body {
    background-color: white;
    width: 750px;
  }
  header {
    width: 100%;
    font-weight: bold;
    padding-bottom: 25px;
    margin-bottom: 8px;
    font-size: 75px;
    color: white;
    background-color: rgb(66, 76, 87);
    position:fixed;
    top: 0;
    left: 0;
    position: absolute;
    text-align: center;
  }
</style>