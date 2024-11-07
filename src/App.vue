<script setup lang="ts">
import axios from "axios";
import BigNumber from "bignumber.js";
import { get } from "lodash";
import { onMounted, reactive } from "vue";
const state = reactive({
  price: "",
  priceFormatted: "",
});
onMounted(() => {
  console.log("hi");
  axios
    .get("https://data-api.binance.vision/api/v3/ticker/price?symbol=BTCUSDT")
    .then((resp) => {
      const price = get(resp, "data.price");
      state.price = price;
      state.priceFormatted = BigNumber(price).toFormat(2);
    });
});
</script>

<template>
  <div class="flex w-full h-screen items-center justify-center">
    {{ state.priceFormatted }}
  </div>
</template>

<style scoped></style>
