<template>
  <div class="modal" >
    <div class="modal-content">
      <h2>Gruppi</h2>
      <button v-if="ShowButton" class="createGroups" @click="showArea=true; ShowButton=false">+</button>
      <button v-if="ShowButton" class="permission" @click="showAreaPermission=true; ShowButton=false"></button>
      <form action="#">
        <label for="lang"> Gruppi: </label>
        <select name="groups" id="lang" v-model="gruppoCorrente">
          <option  v-for="g in groupss" :value="g" :key="g"> {{ g }} </option>
        </select>
        <button class="deleteGroup" @click.prevent="removeGroup">Rimuovi</button>
      </form>
      <textarea v-model="groupName" v-if="showArea" name="newGroup" maxlength="50" required placeholder="Nome del gruppo..."></textarea>
      <textarea v-model="permission" v-if="showAreaPermission" name="Permission" maxlength="50" required placeholder="Inserisci nome utente..."></textarea>
      <button v-if="showArea" class="addGroup" @click="addGroup(); showArea=false; ShowButton=true" type="submit">Aggiungi</button>
      <button v-if="showArea" class="indietro" @click="showArea=false; ShowButton=true" type="submit">Indietro</button>
      <button v-if="showAreaPermission" class="addGroup" @click="showAreaPermission=false; ShowButton=true" type="submit">Aggiungi</button>
      <button v-if="showAreaPermission" class="indietro" @click="showAreaPermission=false; ShowButton=true" type="submit">Indietro</button>
      <div class="modal-buttons">
        <button id="submitButton" @click="save" >Salva</button>
        <button id="cancelButton" @click="cancel" >Annulla</button>
      </div>
    </div>
  </div>
</template>

<script>
export default{
  props: ["groupss", "showArea", "ShowButton","showAreaPermission"],
  data() {
      return {
        groupName: '',
        gruppoCorrente: '',
        persone: [],
      };
  },
  methods:{
    removeGroup(){
      this.$emit('remove-group',this.gruppoCorrente)
    },
    addGroup(){
      this.$emit('add-group', {
        groupName: this.groupName.trim(),
      },
      this.groupss
      );
      this.groupName = '';
    },
    save() {
        // Logica per creare un gruppo
        this.$emit('save-groups',this.gruppoCorrente);
      },
      cancel() {
        // Logica per eliminare un gruppo
        this.$emit('cancel');
      },
      }
    }

</script>

<style scoped>
* {
  color: black;
}
.addGroup{
  position: fixed;
  background-color: rgb(27, 157, 217);
  cursor: pointer;
  top:60%;
  left:39%;
  transform: translate(-50%, -50%);
  width: 20%;
  border:none;
  height: 40px;
  color: black;
  font-size: 18px;
  border: none;
}
.indietro{
  position: fixed;
  background-color: rgb(217, 217, 217);
  cursor: pointer;
  top:60%;
  left:61%;
  transform: translate(-50%, -50%);
  width: 20%;
  height: 40px;
  color: black;
  font-size: 18px;
  border: none;
}
textarea{
  position: fixed;
  top: 50%;
  left:50%;
  transform: translate(-50%, -50%);
}
.createGroups{
  position: fixed;
  top:50%;
  left:40%;
  transform: translate(-50%, -50%);
  width: 15%;
  height: 15%;
  border: none;
  font-size: 40px;
  background-color: rgb(27, 157, 217);
}
label {
  width: 200 px;  
  color: white;
}
select {
  width: 200px;
  size: 302px;
}
option {
  width: 200px;
  size: 16px;
}
.modal-content {
  width: 92%;
  color: white;
}
.modal {
  width: 500px;
  height: 500px;
  background-color: rgb(66, 76, 87);
  padding: 30px;
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 3%;
  z-index: 123456789;
  border: none;
}
h2 {
  font-weight: bold;
  font-size: 30px;
  color: white;
  text-align: center;
  border: none;
}
.modal-buttons {
  padding-bottom: 5px;
  font-size: 30px;
  width: 100%;
  color: white;
  margin-top: 10px;
  position: relative;
  top: 310px;
  border: none;

}
#submitButton {
  border: 1px solid rgb(66, 76, 87);
  background-color: rgb(27, 157, 217);
  cursor: pointer;
  width: 49%;
  height: 40px;
  color: black;
  font-size: 18px;
  margin-right: 2%;
  border: none;
}
#cancelButton {
  border: 1px solid rgb(66, 76, 87);
  background-color: rgb(217, 217, 217);
  cursor: pointer;
  height: 40px;
  width: 49%;
  color: black;
  font-size: 18px;
  border: none;
}
.permission{
  position: fixed;
  top: 50%;
  left: 60%;
  transform: translate(-50%, -50%);
  width: 15%;
  height: 15%;
  border: none;
  background-color: rgb(27, 157, 217);
  background-image: url("src/images/people.png");
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center center;
  border: none;
}
.deleteGroup{
  background-color: rgb(27, 157, 217);
  border: none;
  cursor: pointer;

}
</style>