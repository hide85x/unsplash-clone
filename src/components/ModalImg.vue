<template>
  <v-dialog overlay-opacity="0.9" v-model="dialog" dark width="600">
    <template>
      <div class="modalImg">
        <div class="header">
          <div class="imgInfo">
            <p>{{ imgToModal.user}}</p>
            <p>{{ imgToModal.createdAt }}</p>
          </div>

          <button class="btn" @click="close">X</button>
        </div>

        <img :src="imgToModal.src" alt="" class="modalImg" />
      </div>
    </template>
  </v-dialog>
</template>

<script>
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
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    .btn {
      align-self: flex-start;
      background: white;
      color: black;
      margin: 2px;
      padding: 2px;
      border-radius: 10%;
      transition: filter 0.3s ease;
      &:hover {
        filter: invert(1);
      }
    }
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
  }
  img {
    width: 60%;
    margin: auto;
    padding: 20px;
  }
}
</style>