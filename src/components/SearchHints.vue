<template>
   <div >
      <h4
        class="result"
        @click="chosenOption"
        v-for="res in results"
        :key="res.id"
      >
        {{ res.alt_description }}
      </h4>
      <img v-if="clickedHint" :src="clickedHint.urls.regular" alt="">
    </div>
</template>

<script>
    export default {
        name: "SearchHints",
        props:{
            results: {
            type: [Object],
            required: true
            } 
        },
        data() {
          return {
            clickedHint: null
          }
        },
        methods: {
                chosenOption(e) {
                  console.log('bang')
                  const foundItem= this.results.find(el=> el.alt_description == e.target.innerText)
                  this.clickedHint= foundItem
                 },

        },
    }
</script>

<style lang="scss" scoped>
    .result {
      font-weight: 300;
      padding: 5px;
      &:hover {
        background: rgba(0, 0, 0, 0.137);
        cursor: pointer;
      }
      
    }
      img {
    border-radius: 5px;
    width: 100%;
  }
</style>