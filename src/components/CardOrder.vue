<script>
export default {
  name: "CardOrder",
  props: {
    order: {
      type: Object,
    },
  },
  computed: {
    toRupiah() {
      const result = new Intl.NumberFormat("id-ID", {
        currency: "IDR",
        style: "currency",
        minimumFractionDigits: 0,
      });
      return result.format(this.order.provider.price);
    },
  },
};
</script>
<template>
  <div class="card shadow">
    <div class="card-header">
      <div>
        <ul>
          <li>{{ order.orderId }}</li>
          <li>{{ order.provider.code + "-" + order.group }}</li>
          <li>{{ order.status }}</li>
        </ul>
      </div>
      <div>
        <h5>Created at : {{ order.createdAt }}</h5>
      </div>
    </div>
    <div class="wrapper">
      <div class="left-side-card">
        <h5 class="gray-text-card">Info User</h5>
        <div class="card-contain">
          <div>
            <h5>{{ order.user.name }}</h5>
            <h5 class="center-text-card">
              {{ order.user.email }}
            </h5>
            <h5>{{ order.user.phoneNumber }}</h5>
          </div>
          <div class="detail-product">
            <div class="line" />
            <div class="t">
              <h5 class="gray-text-card">Provider</h5>
              <h5 class="center-text-card gray-text-card">Paket</h5>
              <h5 class="gray-text-card">Exp</h5>
            </div>
            <div>
              <h5>{{ order.provider.name }}</h5>
              <h5 class="center-text-card">
                {{ order.provider.packet }}
              </h5>
              <h5>{{ order.expiredAt }}</h5>
            </div>
          </div>
        </div>
      </div>
      <div class="price">
        <h4>{{ toRupiah }}</h4>
      </div>
    </div>
  </div>
</template>
<style scoped>
.card {
  margin-top: 15px;
  border: 2px solid #86d0c1;
  border-radius: 8px;
  animation-name: card;
  animation-duration: 0.5s;
  cursor: pointer;
}
@keyframes card {
  from {
    transform: translateX(100%);
  }
  to {
    transform: translateX(0);
  }
}
.card-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  border-bottom: 2px solid #86d0c1;
  padding: 8px 15px;
}
ul {
  display: flex;
  gap: 35px;
  font-size: 15px;
}
ul li:first-child {
  list-style: none;
}
.wrapper {
  display: grid;
  grid-template-columns: auto auto auto;
  align-items: center;
  padding: 20px 25px;
  gap: 50px;
}
.left-side-card {
  grid-column-start: 1;
  grid-column-end: 3;
}
.card-contain {
  margin-top: 10px;
  display: flex;
  justify-content: space-between;
}
.detail-product {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 40px;
}
.line {
  width: 2px;
  height: 100%;
  background-color: gray;
}
.price {
  text-align: right;
  font-size: 32px;
  font-weight: bold;
}
.center-text-card {
  margin-top: 7px;
  margin-bottom: 7px;
}
.gray-text-card {
  color: gray;
}
h5 {
  font-size: 15px;
}
</style>
