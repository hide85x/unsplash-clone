<template>
  <div >
    <autocomplete class="input" style="color:black"  :get-result-value="getResultValue" :search="search"></autocomplete>
  </div>
</template>

<script>
import Autocomplete from "@trevoreyre/autocomplete-vue";

const wikiUrl = 'https://en.wikipedia.org'
const params = 'action=query&list=search&format=json&origin=*'

export default {
  components: {
    Autocomplete,
  },
  data() {
    return {
        results: []
        };
  },
      methods: {
       search(input) {
      const url = `${wikiUrl}/w/api.php?${params}&srsearch=${encodeURI(input)}`
 
      return new Promise((resolve) => {
        if (input.length < 3) {
        this.results.push("DUPA")
          return resolve([{title: "No results found"}])
        }
 
        fetch(url)
          .then((response) => response.json())
          .then((data) => {
            resolve(data.query.search)
          })
      })
    },
 
    // Wikipedia returns a format like this:
    //
    // {
    //   pageid: 12345,
    //   title: 'Article title',
    //   ...
    // }
    //
    // We want to display the title
    getResultValue(result) {
      return result.title
    },
 
    // Open the selected article in
    // a new window
    onSubmit(result) {
      window.open(`${wikiUrl}/wiki/${encodeURI(result.title)}`)
    },
      },
};
</script>

<style lang="scss" scoped>
.input {
    margin: auto;
    width: 50%;
}
</style>