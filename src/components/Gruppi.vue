<template>
    <div class="modal" >
    <div class="modal-content">
      <h2>Seleziona gruppo che vuoi cambiare</h2>
      <button class="aggiungiGruppo">+</button>
      <form action="#">
      <label for="lang">Gruppi</label>
      <select name="groups" id="lang">
        <option value="Privato">{{group}}</option>
        <option value="Privato">Pubblico</option>
      </select>
      <input type="submit" value="Submit" />
</form>
      <div class="modal-buttons">
        <button id="submitButton" @click="save" >Salva</button>
          <button id="cancelButton" @click="cancel" >Annulla</button>
      </div>
    </div>
  </div>
</template>

<script>
export default{
methods:{
    save() {
        // Logica per rimuovere una nota
        this.$emit('save-note', this.nota);
      },
      cancel() {
        // Logica per annullare la rimozione di una nota
        this.$emit('cancel');
      },
      }
    }

</script>