<template>
  <v-app>
    <div class="hero">
      <div class="hero__content">
        <h1>Unsplash</h1>
        <p>
          The internet’s source of
          <a target="blank" href="https://unsplash.com/license"
            >freely-usable images.</a
          >
          Powered by creators everywhere.
        </p>
        <Searchbar />
      </div>
    </div>
  </v-app>
</template>

<script>
import Searchbar from "./components/Searchbar.vue";
export default {
  components: { Searchbar },
  data: () => ({}),
};
</script>

<style lang="scss">
html {
  min-height: 100vh;
}
.hero {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background: url("https://images.pexels.com/photos/3784221/pexels-photo-3784221.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=750&w=1260");
  background-position: center;
  background-size: cover;
  background-repeat: no-repeat;
  background-attachment: fixed;
  min-height: 100vh;
  padding: 5px;
  &__content {
    display: flex;
    flex-direction: column;
    color: white;
    p {
      font-size: 1em;
      width: 60%;
    }
    a {
      color: white !important;
      text-transform: none;
    }
  }
}
</style>
