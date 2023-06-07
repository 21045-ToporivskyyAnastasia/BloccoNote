<template>
  <header>Blocco Note</header>
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
      width: 750px;
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