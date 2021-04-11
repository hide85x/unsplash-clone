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
        createdAt: e.target.attributes['data-created'].nodeValue
      };
    },
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
.modalImg {
  background: rgba(0, 0, 0, 0.712);
  color: white;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  .imgInfo {
    padding: 10px;
    background: rgba(0, 0, 0, 0.527);
    width: 100%;
    p {
      padding: 2px;
      margin: 0;
      font-weight: 300;
    }
  }
  img {
    width: 60%;
    margin: auto;
    padding: 20px;
  }
}
.resultsImg {
  margin-top: 20px;
  background: white;
  border-radius: 5px;
  .item {
    background: transparent;
    padding: 5px;
    display: flex;
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