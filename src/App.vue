<template>
  <header>Blocco Note
    <p class="gruppo">Gruppo:</p>
      <button class="groupScreen" @click="showGroups = true;">{{ this.groups[gindex] == undefined ? "Caricando" : (this.groups[gindex].groupName ?? this.groups[gindex]) }}</button>
  </header>

  <ListaNote
    @add-note="showCreateNote = true"
    @modifica-nota="openeditpopup"
    @confirm-remove="openremovepopup"
    :notes="filteredNotes"
  />
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
  <Gruppi
    v-if="showGroups"
    :groupss="groups"
    :gruppi="lastclickedGroup"
    @cancel="showGroups=false"
    :showArea = "false"
    :showOperators = "false"
    :ShowButton = "true"
    @add-group="addGroup"
    @save-groups="changeGroup"
    @remove-group="removeGroup"
    @add-operator="addOperator"
    :operators="operator"
    :currentOperato= "currentOperator"
  />
  <BarraRicerca 
    @search-notes="filterNotes" 
  />
</template>

<script>

//importazione dei componenti per la visualizzazione
import BarraRicerca from "./components/BarraRicerca.vue";
import CreaNota from "./components/CreaNota.vue";
import ListaNote from "./components/ListaNote.vue";
import RimuoviNota from "./components/RimuoviNota.vue";
import ModificaNota from "./components/ModificaNota.vue";
import Gruppi from "./components/Gruppi.vue";
import axios from "axios";
import { toRaw } from "vue";
export default {
  name: "App",
  components: {
    BarraRicerca,
    CreaNota,
    ListaNote,
    RimuoviNota,
    ModificaNota,
    Gruppi,
  },
  mounted(){
    sessionStorage.setItem('operatorID', 20);
    sessionStorage.setItem('operatorName', 'anastasia');
    sessionStorage.setItem('operatorSurname', 'boh');
    console.log(this.groups);
    
    setTimeout(() => {
      //window.location.reload();
      this.aggiornaNotes();
    }, 2000);
  },
  data() {
    return {
      showModificaNote: false,  
      showCreateNote: false,
      showRemoveNote: false,
      showGroups: false,
      notes: [],
      groups: [],
      gindex: 0,
      lastclickedNote: null,
      lastclickedGroup:null,
      query: '',
      currentOperator: sessionStorage.getItem('operatorID'),
    };
  },
  beforeMount() {
    this.notes = [];
    this.groups = [];
    this.readNotes();
    this.readGroups();
    //this.groups = [{groupName: 'Privato',groupOperators: [sessionStorage.getItem('operatorID')]}, {groupName: 'Pubblico',groupOperators: null}];
    console.log(this.groups)
    //this.writeGroups();
    //console.log(this.notes);
    this.getOperators();
    
  },
  computed: {
    filteredNotes() {
      if (this.query === "") return this.notes;

      const lowerCaseQuery = this.query.toLowerCase();

      const newNotes = this.notes.filter((note) =>
        note.title.toLowerCase().includes(lowerCaseQuery) ||
        note.content.toLowerCase().includes(lowerCaseQuery) 
      );
      this.aggiornaNotes();
      return newNotes;
    }
  },
  methods: {
    filterNotes(query) {
      this.query = query;
    },
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
    //metodo read notes per permettere di scrivere nel database
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
    async writeGroups(){
      let data = JSON.stringify({
        "appCode": "ONOINT-0001",
        "dataName": "groups",
        "dataValue": JSON.stringify({ groups: this.groups }),
      });

      let config = {
        method: 'post',
        maxBodyLength: Infinity,
        url: 'http://64.227.120.171:7576/grpc/SetONOAppData',
        headers: { 
          'Content-Type': 'application/json', 
          'Authorization': 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6LTEsImlzcyI6Im9ub1NlcnZlciIsInN1YiI6InNvbWVvbmUiLCJleHAiOjE2ODYzMDQwMDksIm5iZiI6MTY4NjIxOTQwOSwiaWF0IjoxNjg2MjE3NjA5LCJqdGkiOiJvbm8tc2VydmVyIn0.VtfbfToSXSekUVEKtViannwS2O4MUdkLKlQsqpuOnUY'
        },
        data : data
      };

      axios.request(config)
      .then((response) => {
        console.log(JSON.stringify(response.data));
      })
      .catch((error) => {
        console.log(error);
      });
    },
    async readGroups(){
      let data = JSON.stringify({
        "appCode": "ONOINT-0001",
        "dataName": "groups"
      });

      let config = {
        method: 'post',
        maxBodyLength: Infinity,
        url: 'http://64.227.120.171:7576/grpc/GetONOAppDataFromCode',
        headers: { 
          'Content-Type': 'application/json', 
          'Authorization': 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6LTEsImlzcyI6Im9ub1NlcnZlciIsInN1YiI6InNvbWVvbmUiLCJleHAiOjE2ODYzMDQwMDksIm5iZiI6MTY4NjIxOTQwOSwiaWF0IjoxNjg2MjE3NjA5LCJqdGkiOiJvbm8tc2VydmVyIn0.VtfbfToSXSekUVEKtViannwS2O4MUdkLKlQsqpuOnUY'
        },
        data : data
      };

      let risposta = await axios.request(config);
      this.groups=JSON.parse(risposta.data.data.data).groups;
      this.idNelDB();
      this.aggiornaNotes();
    },
    aggiornaNotes(){
      this.notes.forEach(element => {
        if(this.groups[this.gindex].groupName == "Privato"){
          if(element.groupped == this.groups[this.gindex].groupName && element.operatorID == this.currentOperator){
            console.log("if1")
            console.log(this.groups[this.gindex].groupName);
            console.log(element.groupped);
            element.view = true;
          } else {
            element.view = false; 
          }
        } else if(this.groups[this.gindex].groupName == "Pubblico"){
          if(element.groupped == this.groups[this.gindex].groupName){
            console.log("if2")
            console.log(this.groups[this.gindex].groupName);
            console.log(element.groupped);
            element.view = true;
          } else {
            element.view = false; 
          }
        } else if(element.groupped == this.groups[this.gindex].groupName){
            console.log("if3")
            console.log(this.groups[this.gindex].groupName);
            console.log(element.groupped);
            element.view = true;
        } else {
            console.log("if4")
            console.log(this.groups[this.gindex].groupName);
            console.log(element.groupped);
            element.view = false; 
        }/*
        if (element.groupped == this.groups[this.gindex].groupName) {
          //console.log("dentro")
          element.view = true;
          if (this.groups[this.gindex].groupName == "Privato" && element.operatorID == this.currentOperator) {
            console.log(element.operatorID)
            console.log(this.currentOperator)
            element.view = true;
            console.log("if1")
          } else if (this.groups[this.gindex].groupName == "Pubblico") {
            console.log("if2")
            element.view = true;
          } else if(!this.groups[this.gindex].groupOperators.some(e => e == element.operatorID)) {
            console.log("if3")
            element.view = false;
          } else {
            element.view = false;
          }
        } else {
          element.view = false;
        }*/
      });
    },
    idNelDB(){
      console.log(this.groups[0].groupOperators);
      this.groups[0].groupOperators = [sessionStorage.getItem('operatorID')]
      console.log(this.groups[0].groupOperators);
      this.writeGroups();
      this.aggiornaNotes();
    },
    //metodo getOperators
    async getOperators(){
      let data = JSON.stringify({
        "appCode" : "ONOINT-0002",
      });

      let config = {
        method: 'post',
        maxBodyLength: Infinity,
        url: "http://64.227.120.171:7576/grpc/GetOperators",
        headers: {
          'Content-Type': 'application/json',
          'Authorization': 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6LTEsImlzcyI6Im9ub1NlcnZlciIsInN1YiI6InNvbWVvbmUiLCJleHAiOjE2ODYzMDQwMDksIm5iZiI6MTY4NjIxOTQwOSwiaWF0IjoxNjg2MjE3NjA5LCJqdGkiOiJvbm8tc2VydmVyIn0.VtfbfToSXSekUVEKtViannwS2O4MUdkLKlQsqpuOnUY'
        },
        data: data

      }

      let risposta = await axios.request(config);
      console.log(risposta.data.operators, "operatori");
      this.operator = risposta.data.operators;
    },
    addOperator(gruppoCorrente, op){
      console.log(gruppoCorrente)
      if(gruppoCorrente.groupName != 'Privato' && gruppoCorrente.groupName != 'Pubblico'){
        const gruppoPointer = this.groups.find( g => JSON.stringify(g) == JSON.stringify(gruppoCorrente));
        gruppoPointer.groupOperators.push(op);
        this.writeGroups();
        console.log(gruppoCorrente);
      }
    },
    //metodo che aggiunge i gruppi
    addGroup(gruppo, gruppi){
      console.log(gruppo, gruppi, "0");
      if(gruppo.groupName != "" && !this.groups.some( g => g == gruppo.groupName)){
      gruppo.groupOperators.push(this.currentOperator);
      this.groups = gruppi;
      this.groups.push(gruppo);
      this.writeGroups();
      }
      console.log(gruppi, "1", this.groups, "2");
    },
    //metodo per modificare una nota 
    modificaNota(notem, vecchiaNota) {
      let newNote = vecchiaNota;

      newNote.id = notem.id;
      newNote.title = notem.title;
      newNote.content = notem.content;
      newNote.date = ""+notem.date.getDate().toString().padStart(2, '0')+"-"+(notem.date.getMonth() + 1).toString().padStart(2, '0')+"-"+notem.date.getFullYear();

      this.showModificaNote = false;
      this.notes.unshift(newNote);
      //cancellazione della vecchia nota che è stata modificata
      const index = this.notes.findIndex(checkid);
      function checkid(noter) {
        return noter.id == vecchiaNota.id;
      }
      this.notes.splice(index, 1);
      this.writeNotes();
    },
    //cambia il gruppo selezionato 
    changeGroup(gruppo) {
      const  gruppoPointer = this.groups.find(g => g == gruppo);
      
      this.gindex = this.groups.indexOf(gruppoPointer);

      this.aggiornaNotes();
      this.showGroups= false;
    },
    //rimuovi gruppo corrente
    removeGroup(gruppo)
    {
      const  gruppoPointer = this.groups.find(g => g == gruppo);
      //console.log(gruppoPointer);
      if(gruppoPointer!="Privato" && gruppoPointer!="Pubblico")
      {
        this.groups = this.groups.filter(g => g!=gruppoPointer);
        this.notes = this.notes.filter(n => n.groupped != gruppo);
        this.writeGroups();
        this.writeNotes();
        this.changeGroup("Privato")
    }
    },
    //metodo per rimuovere la nota una volta confermato il controllo della rimozione
    removeNote(note) {
      console.log(this.groups);
      const index = this.notes.findIndex(checkid);
      function checkid(noter) {
        return noter.id == note.id;
      }
      this.notes.splice(index, 1);
      this.showRemoveNote = false;
      this.writeNotes();
    },
    //si apre il pop-up per rimuovere una not
    openremovepopup(note) {
      this.lastclickedNote = note;
      this.showRemoveNote = true;
    },
    //si apre il pop-up per editare una nota
    openeditpopup(note) {
      this.lastclickedNote = note;
      this.showModificaNote = true;
    },
    //metodo per aggiungere una nota
    addNote(notem) {
      const note = {
        id: notem.id,
        title: notem.title,
        content: notem.content,
        date: ""+notem.date.getDate().toString().padStart(2, '0')+"-"+(notem.date.getMonth() + 1).toString().padStart(2, '0')+"-"+notem.date.getFullYear(),
        operatorID: this.currentOperator,
        operatorName: sessionStorage.getItem("operatorName"),
        operatorSurname: sessionStorage.getItem("operatorSurname"),
        view: true,
        groupped: this.groups[this.gindex].groupName,
      };
      console.log(note.groupped)
      this.notes.unshift(note);
      this.showCreateNote = false;
      this.showModificaNote = false;
      //console.log(this.notes);
      this.writeNotes();
    },
  },
};
</script>
<!--design del blocco note con css-->
<style>
textarea{
  resize: none;
}
html {
  width: 100%;
  height: 100%;
}
#app {
  width: 100%;
  height: 0;
  padding: 0;
  margin: 0;
}
body {
  background-color: white;
  width: 100vw;
  height: 100vh;
  margin: 0;
}
header {
  width: 100%;
  font-weight: bold;
  padding-bottom: 5px;
  font-size: 60px;
  color: white;
  background-color: rgb(66, 76, 87);
  position: fixed;
  top: 0;
  left: 0;
  position: absolute;
  text-align: center;
}
.gruppo{
  position: absolute;
  top: 0;
  left: 80%;
  font-size: 16px;

}
.groupScreen {
  position: absolute;
  top: 25px;
  left: 80%;
  background-color: rgb(27, 157, 217);
  border: none;
  font-size: 16px;
  width: 100px;
}
</style>