<script>
export default {
  name: "PaginationComponent",
  props: {
    maxVisibleButtons: {
      type: Number,
      required: false,
      default: 5,
    },
    totalPages: {
      type: Number,
      required: true,
    },
    perPage: {
      type: Number,
      required: true,
    },
    currentPage: {
      type: Number,
      required: true,
    },
  },
  computed: {
    numberPages() {
      return Math.ceil(this.totalPages / this.perPage);
    },
  },
  methods: {
    onClickPreviousPage() {
      this.$emit("pageChanged", this.currentPage - 1);
    },
    onClickPage(page) {
      this.$emit("pageChanged", page);
    },
    onClickNextPage() {
      this.$emit("pageChanged", this.currentPage + 1);
    },
  },
};
</script>
<template>
  <div class="pagination">
    <ul>
      <li :class="{ hidden: currentPage <= 1 }" @click="onClickPreviousPage">
        &#10096;
      </li>
      <li
        v-for="(page, index) in new Array(numberPages)"
        :key="index"
        :class="{ active: index + 1 === currentPage }"
        @click="onClickPage(index + 1)"
      >
        {{ index + 1 }}
      </li>
      <li
        :class="{ hidden: currentPage >= numberPages }"
        @click="onClickNextPage"
      >
        &#10097;
      </li>
    </ul>
  </div>
</template>

<style scoped>
.pagination {
  position: absolute;
  right: 0;
  bottom: 0;
}
.pagination ul {
  display: flex;
  gap: 5px;
}
.pagination ul li {
  font-family: monospace;
  list-style: none;
  cursor: pointer;
  border-radius: 100%;
  padding: 10px 13px;
  font-size: 15px;
  font-weight: bold;
  box-shadow: 1px 1px 1px 1px rgba(0 0 0 / 0.2);
}
ul li:hover {
  background-color: #86d0c1;
  color: white;
}
.active {
  background-color: #86d0c1;
  color: white;
}
.hidden {
  display: none;
}
button {
  border: none;
}
</style>
