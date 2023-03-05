<template>
  <div :class="{ backgroundWoman: data.woman, backgroundMan: data.man, backgroundUnavaliable: data.unavaliable }" id="background"></div>
</template>

<script>
export default {
  name: "ProductBackgroundShow",
  props: ["dataComponent"],
  data() {
    return {
      title: "data",
      data: this.dataComponent,
    };
  },
};
</script>