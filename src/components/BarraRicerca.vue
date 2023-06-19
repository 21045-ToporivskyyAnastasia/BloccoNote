<template>
    <div class="search-bar">
      <input type="text" v-model="searchQuery" placeholder="Cerca..." @input="searchNotes" />
    </div>
  </template>
  
  <script>
  export default {
    name: "BarraRicerca",
    data() {
      return {
        searchQuery: "",
      };
    },
    methods: {
      searchNotes() {
        this.$emit("search-notes", this.searchQuery);
      },
    },
  };
  </script>
  
  <style scoped>
  .search-bar {
    margin-bottom: 20px;
    position: absolute;
    top:105px;
    left:9%;
    justify-content: center;
  }
  input {
    padding: 8px;
    width: 245px;
    font-size: 16px;
    z-index:0;
  }
  </style>
  