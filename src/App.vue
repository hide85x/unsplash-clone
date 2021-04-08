<template>
  <v-app>
   
    <div class="hero">
      <div class="hero__content">
        <h1>Unsplash</h1>
        <p>
          The internet’s source of freely-usable images. Powered by creators
          everywhere.
        </p>
      </div>
      <Autocompletenpm />
    </div>
  </v-app>
</template>

<script>
import Autocompletenpm from "./components/Autocompletenpm.vue";
export default {
  components: { Autocompletenpm },
  data: () => ({
    
  }),
};
</script>

<style lang="scss">
.hero {
  background: url("https://images.pexels.com/photos/3784221/pexels-photo-3784221.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=750&w=1260");
  background-position: top;
  background-size: cover;
  margin: auto;
  width: 100%;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: stretch;
  &__content {
    color: white;
    width: 50%;
    margin: 0 auto;
    p {
      font-size: 0.9em;
    }
  }
}
</style>
