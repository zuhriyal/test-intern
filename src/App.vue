<script>
import HeaderSide from "./components/Header.vue";
import SideMenu from "./components/SideMenu.vue";
import FilterItem from "./components/FilterItem.vue";
import OrderList from "./components/OrderList.vue";

export default {
  components: {
    HeaderSide,
    SideMenu,
    FilterItem,
    OrderList,
  },

  data() {
    return {
      orders: {
        data: [],
        pagination: {
          currentPage: 0,
          perPage: 0,
          totalPages: 0,
        },
      },
      paramGetOrderList: {
        currentPage: 1,
        perPage: 5,
      },
      userName: "",
      filterProvider: "All",
      sortProvider: "Sort",
    };
  },
  created() {
    this.getOrderList();
  },
  methods: {
    async getOrderList() {
      const startIndex =
        (this.paramGetOrderList.currentPage - 1) *
        this.paramGetOrderList.perPage;
      const endIndex =
        this.paramGetOrderList.currentPage * this.paramGetOrderList.perPage;

      const response = await fetch(
        "http://demo2378145.mockable.io/seakun-intern-fe"
      );
      const result = await response.json();

      let dataOrd = [];

      if (this.filterProvider === "All") {
        dataOrd = result.data.sort((a, b) =>
          a.createdAt < b.createdAt ? 1 : -1
        );
        if (this.sortProvider === "DESC") {
          dataOrd = result.data.sort((a, b) =>
            a.createdAt > b.createdAt ? 1 : -1
          );
        }
      } else {
        dataOrd = result.data
          .filter((d) => d.provider.name == this.filterProvider)
          .sort((a, b) => (a.createdAt < b.createdAt ? 1 : -1));
        if (this.sortProvider === "DESC") {
          dataOrd = result.data
            .filter((d) => d.provider.name == this.filterProvider)
            .sort((a, b) => (a.createdAt > b.createdAt ? 1 : -1));
        }
      }

      this.orders = {
        ...this.orders,
        data: dataOrd.slice(startIndex, endIndex),
        pagination: {
          totalPages: dataOrd.length,
          perPage: this.paramGetOrderList.perPage,
          currentPage: this.paramGetOrderList.currentPage,
        },
      };
    },
    clickPagination(page) {
      if (this.userName != "") {
        this.paramGetOrderList = {
          ...this.paramGetOrderList,
          currentPage: page,
        };
        this.getOrderListByUserName();
      } else {
        this.paramGetOrderList = {
          ...this.paramGetOrderList,
          currentPage: page,
        };
        this.getOrderList();
      }
    },
    changeUserName(query) {
      this.userName = query;
      this.paramGetOrderList = { ...this.paramGetOrderList, currentPage: 1 };
      this.getOrderListByUserName();
    },
    changeProvider(value) {
      this.filterProvider = value;
      this.paramGetOrderList = { ...this.paramGetOrderList, currentPage: 1 };
      this.getOrderList();
    },
    changeSortProvider(value) {
      this.sortProvider = value;
      this.paramGetOrderList = { ...this.paramGetOrderList, currentPage: 1 };
      this.getOrderList();
    },
    async getOrderListByUserName() {
      const startIndex =
        (this.paramGetOrderList.currentPage - 1) *
        this.paramGetOrderList.perPage;
      const endIndex =
        this.paramGetOrderList.currentPage * this.paramGetOrderList.perPage;

      const response = await fetch(
        "http://demo2378145.mockable.io/seakun-intern-fe"
      );
      const result = await response.json();

      let dataOrd = [];

      if (!this.userName || this.userName.length > 0) {
        dataOrd = result.data.filter(
          (d) =>
            d.user.name.toLowerCase().indexOf(this.userName.toLowerCase()) >= 0
        );
      } else {
        dataOrd = result.data;
      }
      this.orders = {
        ...this.orders,
        data: dataOrd.slice(startIndex, endIndex),
        pagination: {
          totalPages: dataOrd.length,
          perPage: this.paramGetOrderList.perPage,
          currentPage: this.paramGetOrderList.currentPage,
        },
      };
    },
  },
};
</script>

<template>
  <HeaderSide />
  <div class="hero">
    <SideMenu />
    <div class="container">
      <FilterItem
        @changeUserName="changeUserName"
        @changeProvider="changeProvider"
        @changeSortProvider="changeSortProvider"
      />
      <OrderList
        :items="orders"
        :pagination="orders.pagination"
        @clickPagination="clickPagination"
      />
    </div>
  </div>
</template>

<style scoped>
.hero {
  margin: 55px 0 0 0;
  width: 100%;
  display: flex;
}
.container {
  width: 100%;
  padding: 5px 20px;
}
</style>
