<script>
export default {
  name: "FilterItem",
  data() {
    return {
      dataProvider: [
        "Netflix",
        "Canva",
        "Youtube",
        "Nintendo Switch",
        "Hbo Go",
        "Apple One",
        "Mirosoft 365",
        "Prime Video",
        "Gramedia Digital",
        "Nord VPN",
        "Spotify",
        "Freepik",
      ],
      queryUserName: "",
      selectedProvider: "All",
      dataSortProvider: ["ASC", "DESC"],
      selectedSortProvider: "Sort",
    };
  },
  methods: {
    changeProvider(event) {
      this.$emit("changeProvider", event.target.value);
    },
    changeSortProvider(event) {
      this.$emit("changeSortProvider", event.target.value);
    },
    changeUserName(q) {
      this.$emit("changeUserName", q.target.value);
    },
  },
};
</script>
<template>
  <div>
    <h1>Order List</h1>
    <div class="filter-item">
      <section class="search-select">
        <input
          v-model="queryUserName"
          type="text"
          placeholder="Search user name"
          @keypress="changeUserName"
        />
        <button type="submit" @click="changeUserName">Submit</button>
      </section>
      <section class="search-select">
        <select v-model="selectedProvider" @change="changeProvider">
          <option value="All">All</option>
          <option
            v-for="provider in dataProvider"
            :key="provider"
            :value="provider"
          >
            {{ provider }}
          </option>
        </select>
        <select v-model="selectedSortProvider" @change="changeSortProvider">
          <option value="Sort">Sort</option>
          <option v-for="sort in dataSortProvider" :key="sort" :value="sort">
            {{ sort }}
          </option>
        </select>
      </section>
    </div>
  </div>
</template>
<style scoped>
h1 {
  color: #86d0c1;
}

.filter-item {
  margin-top: 10px;
  display: flex;
  justify-content: space-between;
}
section {
  display: flex;
  gap: 7px;
}
select,
button,
input {
  border-radius: 3px;
  border: 1px solid #86d0c1;
  color: #86d0c1;
  background-color: white;
  padding: 3px 5px;
  font-size: 13px;
}
select,
button {
  cursor: pointer;
  background-color: white;
}
select,
button:hover {
  background-color: #86d0c1;
  color: white;
}
input:focus {
  outline: none;
  color: black;
}
</style>
