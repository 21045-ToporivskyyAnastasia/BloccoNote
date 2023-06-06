<template>
  <h1>Blocco Note</h1>
  <ListaNote @add-note="showCreateNote=true" :notes="notes" ></ListaNote>
  <RimuoviNota @confirm-remove="$showRemoveNote=true"/>
  <CreaNota v-if="showCreateNote" @add-note="addNote" @cancel="showCreateNote=false"/>
</template>

<!--scemo stai zitto-->
<!--ammazzati stronzo-->
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
            this.notes = this.notes.filter(note => note.id !== this.noteToRemove);
          this.noteToRemove = null;
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