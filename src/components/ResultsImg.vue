<template>
  <div class="resultsImg" ref="resultsImg">
    <div class="item" v-for="item in results" :key="item.id">
      <!-- <h5>{{ item.description }}</h5> -->
      <img :src="item.urls.regular" alt="" />
    </div>
  </div>
</template>

<script>
import Macy from "macy";

export default {
  name: "ResultsImg",
  props: {
    results: {
      type: [Object],
      required: true,
    },
  },
  data() {
    return {
      macy: null,
    };
  },
  mounted() {
    this.macy = new Macy({
      container: this.$refs["resultsImg"],
      trueOrder: false,
      waitForImages: true,
      margin: 0,
      columns: 3,
      breakAt: {
        1200: 4,
        940: 3,
        520: 2,
        400: 1,
      },
    });
  },
};
</script>

<style lang="scss" scoped>
.resultsImg {
  margin-top: 20px;
  background: white;
  border-radius: 25px;
  .item {
    background: transparent;
    display: flex;
    &:hover {
      box-shadow: 0 0 20px 10000px rgba(0, 0, 0, 0.781);
      z-index: 2;
      border-radius: 25px;
      cursor: pointer;
    }
  }
  img {
    width: 100%;
    padding: 5px;
    border-radius: 25px;
  }
}
</style>