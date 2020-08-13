<template>
  <div id="app">
    <b-container fluid="sm">
      <div class="house-container mx-auto">
        <b-row align-h="end">
          <b-col cols="4">
            <div id="sun" class="rounded-circle mt-3"></div>
          </b-col>
        </b-row>
        <b-row class="d-flex justify-content-center mx-0">
          <div id="roof" class="d-flex">
            <div class="triangle left"></div>
            <div class="triangle seam"></div>
            <div class="triangle right"></div>
          </div>
        </b-row>
        <b-row class="mx-0">
          <div id="house-base" class="mx-auto">
            <b-row>
              <b-col v-for="(i, index) in 2" :key="index">
                <div class="window rounded-circle mt-3">
                </div>
              </b-col>
            </b-row>
          </div>
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
#sun {
  position: relative;
  width: 100px;
  height: 100px;
  background-color: #fbff00;
}
.house-container {
  max-width: 450px;
  max-height: 600px;
}
#roof {
  width: 95%;
  height: 200px;
}
.triangle {
  width: 50%;
  height: 100%;
}
.triangle.left {
  background-image: linear-gradient(to left top, #dc7f69 0%, #dc7f69 50%, transparent 50%);
}
.triangle.right {
  background-image: linear-gradient(to right top, #dc7f69 0%, #dc7f69 50%, transparent 50%);
}
.triangle.seam{
  width: 2px;
  margin: 0 -1px;
  border-radius: 30px;
  background-color: #dc7f69;
}

#house-base {
  position: relative;
  width: 95%;
  height: 200px;
  background-color: #cccccc;
}
.window {
  display: inline-block;
  width: 90px;
  height: 90px;
  border: 5px solid #a2c5e9;
  background-color: #d0e1f4;
  transition: background-color 0.5s ease;
  z-index: 50;
}
</style>
