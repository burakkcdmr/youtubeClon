<template>
  <div>
    <form class="searchForm" @submit.prevent="handleSubmit">
      <input type="text" class="searchInput" v-model="searchTerm" />
      <button class="searchButton">Ara</button>
    </form>
  </div>
</template>

<script>
export default {
  emits: ["termChange"],
  data() {
    return {
      searchTerm: "",
    };
  },

  methods: {
    handleSubmit() {
      this.$emit("termChange", this.searchTerm);
      this.searchTerm = "";
    },
  },
};
</script>

<style scoped>
.searchForm {
  display: flex;
  margin: 20px 0px;
}
.searchInput {
  width: 85%;
  padding: 8px;
  margin-right: 20px;
  border-radius: 20px;
}

.searchButton {
  width: 15%;
  border: none;
  background: green;
  color: white;
  font-size: 18px;
  border-radius: 20px;
  cursor: pointer;
}
</style>
