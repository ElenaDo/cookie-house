<template>
  <div id="app" :class="!daytime ? 'dark-mode' : 'light-mode'">
      <div class="overlay vw-100 vh-100">
      </div>
      <div class="house-container mx-auto">
        <b-row align-h="end" class="mx-0" id="sun-row">
          <b-col cols="col-md-auto mr-1">
            <div id="sun" @click="daytime = !daytime" class="rounded-circle mx-auto mt-3"></div>
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
            <b-row class="mx-0">
              <div id="bakery-name" class="mt-n4 mx-auto">
                <h5 class="text-uppercase font-weight-bold">cookie bakery</h5>
              </div>
            </b-row>
            <b-row class="mx-0">
              <b-col v-for="(i, index) in 2" :key="index">
                <div class="window rounded-circle mt-3">
                  <div class="cookie">
                  </div>
                </div>
              </b-col>
            </b-row>
            <b-row class="door-row mx-0" align-h="end">
              <b-col cols="4">
                <div id="door" @click="createOrder()" class="d-flex align-items-center">
                  <div id="door-handle" class="rounded ml-1">
                  </div>
                </div>
              </b-col>
              <b-col cols="4" class="pl-0 pt-3" :class="[{'animate__animated': fallenBox,
              'animate__swing': fallenBox,
              'mailbox_fallen': fallenBox}]">
                <div id="mailbox" @click="fallenBox = true" class="pt-2">
                  <div id="mailbox-cap" class="mx-auto"></div>
                  <span>Mailbox</span>
                </div>
              </b-col>
            </b-row>
          </div>
        </b-row>
      </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {
  },
  data: () => ({
    daytime: true,
    fallenBox: false,
  }),
  methods: {
    async createOrder() {
      let ok;
      const host = process.env.VUE_APP_HOST || 'http://localhost:8000';
      try {
        const response = await fetch(host, { method: 'POST' });
        const result = await response;
        if (result.ok) ok = true;
      } catch (err) {
        console.log(err);
      }

      let title = 'Thank you!';
      let message = 'Your order has been placed';
      let variant = 'info';
      if (!ok) {
        title = 'Try again later';
        message = 'Something went wrong';
        variant = 'danger';
      }
      this.makeToast(title, message, variant);
    },
    makeToast(title, message, variant) {
      this.$bvToast.toast(message, {
        title,
        autoHideDelay: 3000,
        appendToast: false,
        variant,
        toaster: 'b-toaster-bottom-center',
      });
    },
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
}
.light-mode {
  background-color: transparent;
}
.dark-mode{
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
}
div.overlay {
  position: absolute;
  z-index: -1;
  transition: 1s ease;
}
.dark-mode div.overlay {
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 50;
}
#sun {
  position: relative;
  width: 100px;
  height: 100px;
  background-color: #fbff00;
  z-index: 101;
  cursor: pointer;
}
#sun-row {
  height: 100px;
}
.house-container {
  max-width: 450px;
  max-height: 100vh;
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
  height: auto;
  background-color: #cccccc;
}
#bakery-name {
  width: 200px;
  height: 50px;
  color: #2d5814;
  background-color: #90c678;
  border: 3px solid #6bad4c;
}
#bakery-name h5{
  line-height: 50px;
}
.window {
  display: inline-block;
  width: 90px;
  height: 90px;
  border: 5px solid #a2c5e9;
  background-color: #d0e1f4;
  z-index: 50;
}
.window:hover{
  background-color: transparent;
  border: none;
}
.cookie {
  background: url("../public/cookie.png");
  opacity: 0;
  background-size: cover;
  height: 100%;
  width: 100%;
  transition: opacity 0.3s;
}
.window:hover .cookie{
  opacity: 1;
}
.door-row{
  min-height: 130px;
  overflow: visible;
}
#door {
  position: absolute;
  margin: 0 auto;
  bottom: 0;
  left: 0;
  right: 0;
  height: 130%;
  width: 60%;
  background-color:#f5b465;
  cursor: pointer;
}
#door-handle {
  width: 30px;
  height: 5px;
  background-color: #b46100;
}
#mailbox {
  width: 60%;
  height: 50%;
  background-color: #999;
  bottom: 50px;
  cursor: pointer;
  transition: bottom 0.5s ease-in;
}
.mailbox_fallen #mailbox{
  position: absolute;
  bottom: 0;
  cursor: auto;
}
#mailbox-cap {
  width: 80%;
  height: 10%;
  background-color: #656565;
}
#mailbox span {
  font-size: 80%;
}
</style>
