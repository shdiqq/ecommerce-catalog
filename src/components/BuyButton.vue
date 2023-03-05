<template>
  <div :class="{ buyButtonWoman: woman, buyButtonMan: man }" id="buyButton">
    <button>Buy now</button>
  </div>
</template>

<script>
export default {
  name: "BuyButtonShow",
  props: ["woman", "man"],
};
</script>