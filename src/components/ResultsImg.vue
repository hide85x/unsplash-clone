<template>
  <div>
    <div class="resultsImg" ref="resultsImg">
      <div class="item" v-for="item in results" :key="item.id">
        <img
          :data-created="item.created_at"
          :data-user="item.user.name"
          @click.stop="dialog = true"
          @click="setModalImg"
          :src="item.urls.regular"
          alt=""
        />
      </div>
    </div>
    <ModalImg
      :results="results"
      :dialog="dialog"
      :imgToModal="imgToModal"
    ></ModalImg>
  </div>
</template>

<script>
import Macy from "macy";
import ModalImg from "./ModalImg.vue";
export default {
  components: { ModalImg },
  name: "ResultsImg",
  props: {
    results: {
      type: [Object],
      required: true,
    },
  },
  data() {
    return {
      dialog: false,
      macy: null,
      imgToModal: null,
    };
  },
  methods: {
    setModalImg(e) {
      console.log(e.target.attributes["data-user"].nodeValue);
      this.imgToModal = {
        user: e.target.attributes["data-user"].nodeValue,
        src: e.target.src,
        createdAt: e.target.attributes["data-created"].nodeValue,
      };
    },
  },
  mounted() {
    this.macy = new Macy({
      container: this.$refs["resultsImg"],
      trueOrder: false,
      waitForImages: true,
      margin: 0,
      columns: 4,
      breakAt: {
        1200: 4,
        940: 4,
        520: 2,
        400: 2,
      },
    });
  },
};
</script>

<style lang="scss" scoped>

.resultsImg {
  margin-top: 20px;
  background: white;
  border-radius: 5px;
  .item {
    background: transparent;
    padding: 5px;
    display: flex;
    width:100%;
    &:hover {
      box-shadow: 0 0 20px 10000px rgba(0, 0, 0, 0.781);
      z-index: 2;
      cursor: pointer;
      border-radius: 5px;
    }
  }
  img {
    border-radius: 5px;
    width: 100%;
  }
}
</style>