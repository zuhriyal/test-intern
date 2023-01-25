<script>
import CardOrder from "./CardOrder.vue";

export default {
  name: "PopupCard",
  components: { CardOrder },
  props: {
    isShow: {
      type: Boolean,
      default: true,
    },
    orderDetails: {
      type: Object,
    },
  },
  methods: {
    closePopup() {
      this.$emit("closePopup");
    },
  },
};
</script>
<template>
  <div v-show="isShow" class="modal">
    <div v-if="orderDetails.payment" class="popup-card shadow">
      <div class="card">
        <h1>Order Detail</h1>
        <div class="modal-wrapper">
          <CardOrder :order="orderDetails" class="card-modal" />
          <div class="payment-details">
            <div class="details transaction-details">
              <h5>Voucher Code</h5>
              <h5>Payment Status</h5>
              <h5>Payment Date</h5>
              <h5>Payment Bank</h5>
            </div>
            <div v-if="orderDetails.payment" class="transaction-details">
              <h5>{{ orderDetails.payment.voucherCode }}</h5>
              <h5>{{ orderDetails.payment.paymentStatus }}</h5>
              <h5>{{ orderDetails.payment.paymentDate }}</h5>
              <h5>{{ orderDetails.payment.paymentBank }}</h5>
            </div>
          </div>
        </div>
        <button class="close-modal" @click="closePopup">Close</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.modal {
  top: 0;
  bottom: 0;
  right: 0;
  left: 0;
  background-color: rgba(12, 12, 12, 0.846);
  position: fixed;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 95;
  box-sizing: border-box;
}
.popup-card {
  height: max-content;
  padding: 10px 20px 60px;
  width: max-content;
  background-color: wheat;
  border-radius: 20px;
  z-index: 99;
  animation: dropModal 0.5s linear;
}
@keyframes dropModal {
  0% {
    transform: translateY(-100%);
  }
  10% {
    transform: translateY(-80%);
  }
  20% {
    transform: translateY(-60%);
  }
  30% {
    transform: translateY(-40%);
  }
  40% {
    transform: translateY(-20%);
  }
  50% {
    transform: translateY(-10%);
  }
  60% {
    transform: translateY(0%);
  }
  70% {
    transform: translateY(3%);
  }
  80% {
    transform: translateY(5%);
  }
  90% {
    transform: translateY(3%);
  }
  100% {
    transform: translateY(0%);
  }
}
.card {
  position: relative;
}
.close-modal {
  padding: 3px 20px;
  position: absolute;
  bottom: -40px;
  right: 0;
  cursor: pointer;
}
.payment-details {
  margin-top: 20px;
  padding: 10px 20px;
  width: 100%;
  display: flex;
  gap: 30px;
  border: 2px solid #86d0c1;
  background-color: white;
  border-radius: 10px;
  animation: payment 0.5s;
}
@keyframes payment {
  from {
    transform: translateX(100%);
  }
  to {
    transform: translateX(0);
  }
}
.details {
  color: gray;
}
.transaction-details {
  display: flex;
  flex-direction: column;
  row-gap: 8px;
}
.card-modal {
  background-color: white;
}
</style>
