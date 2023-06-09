<template>
  <header>Blocco Note</header>
  <ListaNote
    @add-note="showCreateNote = true"
    @modifica-nota="openeditpopup"
    @confirm-remove="openremovepopup"
    :notes="notes"
  ></ListaNote>
  <RimuoviNota
    v-if="showRemoveNote"
    :nota="lastclickedNote"
    @remove-note="removeNote"
    @cancel="showRemoveNote = false"
  />
  <CreaNota
    v-if="showCreateNote"
    @add-note="addNote"
    @cancel="showCreateNote = false"
  />
  <ModificaNota
    v-if="showModificaNote"
    :nota="lastclickedNote"
    @modifica-note="modificaNota"
    @cancel="showModificaNote = false"
  />
</template>

<script>
import CreaNota from "./components/CreaNota.vue";
import ListaNote from "./components/ListaNote.vue";
import RimuoviNota from "./components/RimuoviNota.vue";
import ModificaNota from "./components/ModificaNota.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    CreaNota,
    ListaNote,
    RimuoviNota,
    ModificaNota,
  },
  data() {
    return {
      showModificaNote: false,
      showCreateNote: false,
      showRemoveNote: false,
      notes: [],
      lastclickedNote: null,
    };
  },
  beforeMount() {
    this.notes = [];
    this.readNotes();
    console.log(this.notes);
  },
  methods: {
    async writeNotes() {
      let data = JSON.stringify({
        appCode: "ONOINT-0001",
        dataName: "notes",
        dataValue: JSON.stringify({ notes: this.notes }),
      });

      let config = {
        method: "post",
        maxBodyLength: Infinity,
        url: "http://64.227.120.171:7576/grpc/SetONOAppData",
        headers: {
          "Content-Type": "application/json",
          Authorization:
            "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6LTEsImlzcyI6Im9ub1NlcnZlciIsInN1YiI6InNvbWVvbmUiLCJleHAiOjE2ODYzMDQwMDksIm5iZiI6MTY4NjIxOTQwOSwiaWF0IjoxNjg2MjE3NjA5LCJqdGkiOiJvbm8tc2VydmVyIn0.VtfbfToSXSekUVEKtViannwS2O4MUdkLKlQsqpuOnUY",
        },
        data: data,
      };
      axios
        .request(config)
        .then((response) => {
          console.log(JSON.stringify(response.data));
        })
        .catch((error) => {
          console.log(error);
        });
    },
    async readNotes() {
      let data = JSON.stringify({
        appCode: "ONOINT-0001",
        dataName: "notes",
      });

      let config = {
        method: "post",
        maxBodyLength: Infinity,
        url: "http://64.227.120.171:7576/grpc/GetONOAppDataFromCode",
        headers: {
          "Content-Type": "application/json",
          Authorization:
            "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6LTEsImlzcyI6Im9ub1NlcnZlciIsInN1YiI6InNvbWVvbmUiLCJleHAiOjE2ODYzMDQwMDksIm5iZiI6MTY4NjIxOTQwOSwiaWF0IjoxNjg2MjE3NjA5LCJqdGkiOiJvbm8tc2VydmVyIn0.VtfbfToSXSekUVEKtViannwS2O4MUdkLKlQsqpuOnUY",
        },
        data: data,
      };

      let risposta = await axios.request(config);
      this.notes=JSON.parse(risposta.data.data.data).notes;
    },
    modificaNota(notem, vecchiaNota) {
      const note = {
        id: notem.id,
        title: notem.title,
        content: notem.content,
        date: ""+notem.date.getDate().toString().padStart(2, '0')+"-"+(notem.date.getMonth() + 1).toString().padStart(2, '0')+"-"+notem.date.getFullYear(),
      };
      this.showModificaNote = false;
      this.notes.push(note);
      const index = this.notes.findIndex(checkid);
      function checkid(noter) {
        return noter.id == vecchiaNota.id;
      }
      this.notes.splice(index, 1);
      this.writeNotes();
    },
    removeNote(note) {
      const index = this.notes.findIndex(checkid);
      function checkid(noter) {
        return noter.id == note.id;
      }
      this.notes.splice(index, 1);
      this.showRemoveNote = false;
      this.writeNotes();
    },
    openremovepopup(note) {
      this.lastclickedNote = note;
      this.showRemoveNote = true;
    },
    openeditpopup(note) {
      this.lastclickedNote = note;
      this.showModificaNote = true;
    },
    addNote(notem) {
      const note = {
        id: notem.id,
        title: notem.title,
        content: notem.content,
        date: ""+notem.date.getDate().toString().padStart(2, '0')+"-"+(notem.date.getMonth() + 1).toString().padStart(2, '0')+"-"+notem.date.getFullYear(),
      };
      this.notes.push(note);
      this.showCreateNote = false;
      this.showModificaNote = false;
      console.log(this.notes);
      this.writeNotes();
    },
  },
};
</script>
<style>
* {
  max-width: 750px;
}
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
  position: fixed;
  top: 0;
  left: 0;
  position: absolute;
  text-align: center;
}
</style>
