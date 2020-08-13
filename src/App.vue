<template>
  <div id="app">
    <b-container fluid="sm">
      <div class="house-container mx-auto">
        <b-row align-h="end" class="mx-0">
          <b-col cols="4">
            <div id="sun" class="rounded-circle mt-3 mr-3"></div>
          </b-col>
        </b-row>
      </div>
    </b-container>
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.house-container{
  max-width: 450px;
}
#sun {
  position: relative;
  width: 100px;
  height: 100px;
  background-color: #fbff00;
}
</style>
