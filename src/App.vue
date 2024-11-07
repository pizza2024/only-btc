<script setup lang="ts">
import axios from "axios";
import BigNumber from "bignumber.js";
import { get } from "lodash";
import { onMounted, reactive } from "vue";
const state = reactive({
  price: "",
  priceFormatted: "",
});
function refresh() {
  axios
    .get("https://data-api.binance.vision/api/v3/ticker/price?symbol=BTCUSDT")
    .then((resp) => {
      const price = get(resp, "data.price");
      state.price = price;
      state.priceFormatted = BigNumber(price).toFormat(2);
    });
}
onMounted(() => {
  console.log("hi");
  refresh();
});
</script>

<template>
  <div class="flex w-full h-screen items-center justify-center gap-[1rem] flex-col">
    <div>
      {{ state.priceFormatted }}
    </div>
    <div>
      <button class="border p-2 rounded-xl" @click="refresh">refresh</button>
    </div>
  </div>
</template>

<style scoped></style>
