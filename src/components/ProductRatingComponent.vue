<template>
  <div class="ratingProduct">
    <span>{{ rating }}/5</span>

    <div v-if="category === 'men\'s clothing'">
      <div>
        <ManCircleShow v-for="(rate, index) in Math.floor(rating)" :key="index + rate"/>
        <ManEmptyCircleShow v-for="(rate, index) in 5 - Math.floor(rating)" :key="index + rate"/>
      </div>
    </div>

    <div v-else-if="category === 'women\'s clothing'">
      <div>
        <WomanCircleShow v-for="(rate, index) in Math.floor(rating)" :key="index + rate"/>
        <WomanEmptyCircleShow v-for="(rate, index) in 5 - Math.floor(rating)" :key="index + rate"/>
      </div>
    </div>
  </div>
</template>

<script>
import ManCircleShow from './ManCircle.vue';
import ManEmptyCircleShow from './ManEmptyCircle.vue';
import WomanCircleShow from './WomanCircle.vue';
import WomanEmptyCircleShow from './WomanEmptyCircle.vue';

export default {
  name: "ProductRatingComponentShow",
  components: {
    ManCircleShow,
    ManEmptyCircleShow,
    WomanCircleShow,
    WomanEmptyCircleShow
  },
  props: ["category", "rating"],
};
</script>