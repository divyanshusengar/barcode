<template>
  <v-app>
    <v-system-bar
      app
      color="#8F2F4E"
      dark
    ></v-system-bar>
    <v-main id="bf">
      <v-app-bar
        :dark="!fs"
        flat
        :color="fs ? '#ffffff' : '#ffffff00'"
        absolute
      >
        <v-btn icon>
          <v-icon :dark="!fs" @click="fs = !fs">mdi-chevron-left</v-icon>
        </v-btn>
        <v-list-item
          two-line
          class="px-0"
        >
          <v-list-item-content>
            <v-list-item-title :class="{ 'header-title': fs, 'font-weight-medium': true }">
              Arrivals
            </v-list-item-title>
            <v-list-item-subtitle class="text-caption">
              Terminal 3 • IGI Airport
            </v-list-item-subtitle>
          </v-list-item-content>
          <v-list-item-action :class="{'d-none': !fs, 'text-right': true}">
            <v-list-item-title :class="{ 'header-cart-price': fs, 'font-weight-medium': true }">
              ₹11590
            </v-list-item-title>
            <v-list-item-subtitle class="text-caption">
               Saved : ₹1220
            </v-list-item-subtitle>
          </v-list-item-action>
        </v-list-item>
      </v-app-bar>
      <!-- Scanner -->
      <v-quagga :onDetected="logIt" :readerSize="readerSize" :readerTypes="['ean_reader']"></v-quagga>
      <div class="scanner-icons">
        <v-row
          align="center"
          justify="end"
        >
          <v-col class="text-right">
            <v-fade-transition><span v-if="textSplash" class="pr-2 font-weight-medium icon-splash">Help</span></v-fade-transition><v-icon color="#ffffff">mdi-help-circle-outline</v-icon>
          </v-col>
        </v-row>
        <v-row
          align="center"
          justify="end"
        >
          <v-col class="text-right">
            <v-fade-transition><span v-if="textSplash" class="pr-2 font-weight-medium icon-splash">Flash On</span></v-fade-transition><v-icon color="#ffffff">mdi-flash-outline</v-icon>
          </v-col>
        </v-row><v-row
          align="center"
          justify="end"
        >
          <v-col class="text-right">
            <v-fade-transition><span v-if="textSplash" class="pr-2 font-weight-medium icon-splash">Sound On</span></v-fade-transition><v-icon color="#ffffff">mdi-volume-high</v-icon>
          </v-col>
        </v-row><v-row
          align="center"
          justify="end"
        >
          <v-col class="text-right">
            <v-fade-transition><span v-if="textSplash" class="pr-2 font-weight-medium icon-splash">Enter Barcode</span></v-fade-transition><v-icon color="#ffffff">mdi-barcode</v-icon>
          </v-col>
        </v-row>
      </div>
      <!-- Scanner -->
      <v-bottom-sheet
        v-model="sheet"
        no-click-animation
        persistent
        hide-overlay
        :fullscreen="fs"
        :content-class="fs ? 'v-main-wrap white' : 'white'"
      >
        <v-btn
          v-if="!fs"
          absolute
          dark
          fab
          top
          left
          @click="counter ? fs = true : fs = true"
          color="#8F2F4E"
        >
          <v-badge
            light
            bordered
            color="#8F2F4E"
            :content="counter"
            :value="counter"
            overlap
          >
            <v-img :src="require('@/assets/Group 91.svg')" contain aspect-ratio="1" height="34" width="34"></v-img>
          </v-badge>
        </v-btn>
        <v-row
          v-if="!counter"
          align="end"
          justify="end"
          no-gutters
          class="py-2 pl-2 pr-8"
        >
          <v-col cols="8">
            <div class="font-weight-medium text-center cart-empty-header">Your cart is empty</div>
            <div class="text-center cart-empty-body">Scan barcode of product to add to cart</div>
          </v-col>
        </v-row>
      </v-bottom-sheet>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: 'App',
  data: () => ({
    sheet: true,
    fs: false,
    counter: 0,
    readerSize: {
      width: 640,
      height: 480
    },
    detecteds: [],
    textSplash: true
  }),
  mounted () {
    setTimeout(() => {
      this.textSplash = false
    }, 3000)
  },
  methods: {
    logIt (data) {
      console.log('detected', data)
    }
  }
};
</script>

<style>
#bf {
  background-color: blue;
}
video {
  height: 100% !important;
  width: 100% !important;
}
.scanner, .drawingBuffer {
  height: 100% !important;
  width: 100% !important;
}
.scanner-icons {
  position: fixed;
  right: 16px;
  top: 30%;
}
.icon-splash {
  color: #ffffff;
}
.v-main-wrap {
  margin-top: 80px !important;
  box-shadow: none !important;
}
.header-title {
  color: #8F2F4E;
}
.header-cart-price {
  color: #8F2F4E;
  align-self: inherit !important;
}
.v-dialog__content {
  height: auto !important;
  top: auto !important;
  bottom: 0 !important;
}
.cart-empty-header {
  font-size: 1.2rem;
  color: #8F2F4E;
}
.cart-empty-body {
  font-size: 0.65rem;
  font-weight: 400;
  color: #58595B;
}
</style>
