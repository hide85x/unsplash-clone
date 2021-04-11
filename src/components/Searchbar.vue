<template>
  <div class="searchbar">
    <form @submit.prevent="">
      <input
        placeholder="what do You desire...? "
        @keydown.enter="atEnter"
        type="text"
        v-model="search"
        @input="onChange"
      />
      <div v-if="search" @click="clear" class="clear">X</div>
    </form>
    <transition name="fade">
      <SearchHints
        :results="results"
        v-if="results.length > 0 && !enterPressed"
        class="results"
      >
      </SearchHints>
    </transition>

    <transition name="fade">
      <ResultsImg
        :results="results"
        v-if="results.length > 0 && enterPressed"
      ></ResultsImg>
    </transition>
  </div>
</template>

<script>
import axios from "axios";
import ResultsImg from "./ResultsImg.vue";
import SearchHints from "./SearchHints.vue";

const baseUrl = "https://api.unsplash.com/search/photos?query=";

export default {
  components: { ResultsImg, SearchHints },
  data() {
    return {
      search: "",
      results: [],
      enterPressed: false,
    };
  },
  methods: {
    clear() {
      this.results = [];
      this.search = "";
    },
    atEnter() {
      this.enterPressed = true;
    },
    onChange() {
      this.enterPressed = false;
      this.results = [];
      const urlToHit = `${baseUrl}${encodeURI(this.search)}`;
      return new Promise((resolve) => {
        if (this.search.length < 3) {
          return resolve((this.results = []));
        }
        axios({
          method: "get",
          headers: {
            Authorization:
              "Client-ID maM2dlj4UD2aMFukZYurAv_XTeC7PktBcZo3QR8OF74",
          },
          url: urlToHit,
        })
          .then((res) => {
            console.log(res.data.total);
            if (res.data.total === 0) {
              return resolve(
                this.results.push({ alt_description: "Not found" })
              );
            }
            this.results = res.data.results.map((el) => {
              return el;
            });
          })
          .catch((err) => console.log(err));
      });
    },
  },
};
</script>

<style lang="scss" scoped>
.searchbar {
 width: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  @media (max-width:700px) {
    width: 100%;
  };

  form {
    position: relative;
    display: flex;
    justify-content: stretch;

    .clear {
      color: black;
      font-weight: 700;
      position: absolute;
      right: 20px;
      bottom: 12px;
      transition: all 0.2s ease;
      &:hover {
        transform: scale(1.1);
        cursor: pointer;
      }
    }
    input {
      background: white;
      border-radius: 25px;
      width: 100%;
      height: 50px;
      outline: none;
      padding: 15px;
    }
  }
  .results {
    background: rgb(255, 255, 255);
    color: black;
    padding: 15px;
    border-radius: 25px;
    margin-top: 10px;
  }
}
//animations
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>


