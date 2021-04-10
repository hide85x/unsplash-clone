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
    </div>
</template>

<script>
    export default {
        name: "SearchHints",
        props:{
            results: {
            type: [Object],
            requuied: true
            } 
        },
        methods: {
                chosenOption() {},

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
</style>