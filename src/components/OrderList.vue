<script>
import CardOrder from "./CardOrder.vue";
import Pagination from "./Pagination.vue";
import PopupCard from "./PopupCard.vue";

export default {
  name: "OrderList",
  components: {
    CardOrder,
    Pagination,
    PopupCard,
  },
  props: {
    items: {
      type: Array,
      required: true,
    },
    pagination: {
      type: Object,
    },
  },
  data() {
    return {
      isShow: false,
      orderDetails: {},
    };
  },
  methods: {
    onPageChange(page) {
      this.$emit("clickPagination", page);
    },
    showPopup(item) {
      this.orderDetails = {};
      this.orderDetails = item;
      this.isShow = !this.isShow;
    },
  },
};
</script>
<template>
  <div class="wrapper">
    <div v-for="item in items.data" :key="item.id">
      <CardOrder :order="item" @click="showPopup(item)" />
    </div>
    <PopupCard
      v-if="orderDetails"
      :is-show="isShow"
      :order-details="orderDetails"
      @closePopup="isShow = !isShow"
    />
    <Pagination
      :total-pages="pagination.totalPages"
      :per-page="pagination.perPage"
      :current-page="pagination.currentPage"
      @pageChanged="onPageChange"
    />
  </div>
</template>
<style scoped>
.wrapper {
  position: relative;
  padding-bottom: 60px;
  min-height: calc(100vh - 155px);
}
</style>
