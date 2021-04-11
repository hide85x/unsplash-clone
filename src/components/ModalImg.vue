<template>
  <v-dialog overlay-opacity="0.9" v-model="dialog" dark width="80%">
    <template>
      <div class="modalImg">
        <div class="header">
          <div class="imgInfo">
            <p>taken by {{ imgToModal.user }}</p>
            <p>on {{ dateFormat }}</p>
          </div>

          <button class="btn" @click="close">X</button>
        </div>

        <img :src="imgToModal.src" alt="" class="modalImg" />
      </div>
    </template>
  </v-dialog>
</template>

<script>
import moment from "moment";
export default {
  name: "ModalImg",
  props: {
    dialog: {
      type: Boolean,
      required: true,
    },

    imgToModal: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      dialog: false,
    };
  },
  mounted() {
    console.log(this.imgToModal);
  },
  computed: {
    dateFormat() {
      return moment(new Date(this.imgToModal.createdAt)).format("MMMM YYYY");
    },
  },
  methods: {
    close() {
      this.dialog = false;
    },
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
  .header {
    background: rgba(0, 0, 0, 0.527);
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    .btn {
      align-self: flex-start;
      background: white;
      color: black;
      margin: 2px;
      padding: 10px;
      border-radius: 10%;
      transition: filter 0.3s ease;
      &:hover {
        filter: invert(1);
      }
    }
    .imgInfo {
      padding: 1px;
      width: 100%;
      span {
        text-decoration: underline;
      }
      p {
        padding:0 5px;
        margin: 0;
        font-weight: 300;
        @media (max-width:700px) {
            font-size: 0.6em;
            
        }
      }
    }
  }
  img {
    width: 50%;
    margin:0;
    padding: 10px;
    @media(max-width:700px) {
        width: 100%;
    }
  }
}
</style>