<template>
  <div v-if="isLoading">
    <LoadingShow />
  </div>

  <div v-else>
    <div v-if="!category.unavaliable" class="view">
      <ProductBackgroundShow :dataComponent=category />

      <div class="cardContainer">
        <div class="card">
          <div class="imageProduct">
            <img :src="data.image" />
          </div>

          <div class="contentContainer">
            <div class="titleProduct">
              <div :class="{ colorPalletteWoman: category.woman, colorPalletteMan: category.man, }">
                {{ data.title }}
              </div>
            </div>

            <div class="categoryAndRatingProduct">
              <div class="categoryAndRatingProductContainer">
                <div class="categoryProduct">{{ data.category }}</div>
                <ProductRatingComponentShow :category="data.category" :rating="data.rating.rate" />
              </div>
            </div>

            <div class="descriptionProduct">
              {{ data.description }}
            </div>

            <div class="priceProductAndButton">
              <div class="priceProduct">${{ data.price }}</div>

              <div class="buttonContainer">
                <div class="buttonItem">
                  <BuyButtonShow :woman="category.woman" :man="category.man" />
                </div>

                <div v-if="category.woman" class="buttonItem">
                  <button type="button" @click="getProductFromAPI()" class="nextProduct nextProductWoman">Next
                    Product</button>
                </div>

                <div v-else class="buttonItem">
                  <button type="button" @click="getProductFromAPI()" class="nextProduct nextProductMan">Next
                    Product</button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div v-else class="unavaliableView">
      <ProductBackgroundShow :dataComponent=category />
      <div class="unavaliableCard">
        <div class="unavaliableDescription">This product is unavaliable to show</div>
        <button type="button" @click="getProductFromAPIPreventError()" class="nextButtonUnavaliable">
          Next Product
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import ProductBackgroundShow from './Background.vue';
import BuyButtonShow from "./BuyButton.vue";
import ProductRatingComponentShow from "./ProductRatingComponent.vue";
import LoadingShow from "./Loading.vue";

export default {
  name: 'ProductDisplay',
  components: {
    ProductBackgroundShow,
    BuyButtonShow,
    ProductRatingComponentShow,
    LoadingShow
  },
  data() {
    return {
      title: 'data',
      data: null,
      category: {
        man: null,
        woman: null,
        unavaliable: null,
      },
      isGetError: false,
      isLoading: false,
      indexPage: 1
    }
  },
  methods: {
    async getProductFromAPI() {

      if (this.indexPage === 21) {
        this.indexPage = 1;
      }

      this.isLoading = true;

      const response = await fetch(`https://fakestoreapi.com/products/${this.indexPage}`);
      const data = await response.json();
      let product = { ...data }

      this.indexPage++;

      if (product.category === "men's clothing") {
        this.category.man = true;
        this.category.woman = false;
        this.category.unavaliable = false;
      } else if (product.category === "women's clothing") {
        this.category.man = false;
        this.category.woman = true;
        this.category.unavaliable = false;
      } else {
        this.category.man = false;
        this.category.woman = false;
        this.category.unavaliable = true;
        this.isGetError = true;
      }

      this.data = data;
      this.isLoading = false;
    },
    async getProductFromAPIPreventError(){
      if (this.indexPage === 21) {
        this.indexPage = 1;
      }

      this.isLoading = true;

      while (this.isGetError === true) {
        const response = await fetch(`https://fakestoreapi.com/products/${this.indexPage}`);
        const data = await response.json();
        let product = { ...data }

        this.indexPage++;

        if (product.category === "men's clothing") {
          this.category.man = true;
          this.category.woman = false;
          this.category.unavaliable = false;
          this.isGetError = false;
        } else if (product.category === "women's clothing") {
          this.category.man = false;
          this.category.woman = true;
          this.category.unavaliable = false;
          this.isGetError = false;
        } else {
          this.category.man = false;
          this.category.woman = false;
          this.category.unavaliable = true;
        }
        this.data = data;
      }
      this.isLoading = false;
    }
  },
  mounted() {
    this.getProductFromAPI();
    this.getProductFromAPIPreventError();
  }
}
</script>