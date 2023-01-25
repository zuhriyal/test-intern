<script>
export default {
  name: "HeaderSide",
};
</script>
<template>
  <header class="shadow">
    <h2>Seakun Back-office</h2>
  </header>
</template>
<style scoped>
header {
  width: 100%;
  height: 55px;
  background-color: white;
  display: flex;
  align-items: center;
  padding-left: 20px;
  position: fixed;
  top: 0;
  z-index: 90;
}
h2 {
  font-size: 18px;
  color: #86d0c1;
  cursor: pointer;
}
</style>
