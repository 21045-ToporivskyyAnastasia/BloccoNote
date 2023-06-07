<template>
  <h1>Blocco Note</h1>
  <ListaNote @add-note="showCreateNote=true" @confirm-remove="showRemoveNote=true" :notes="notes" ></ListaNote>
  <RimuoviNota v-if="showRemoveNote" @remove-note="removeNote" />
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