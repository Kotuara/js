<template>
  <div id="app">
    <div id="first">
      <h2> Сканирование камерой (или с фотографии) </h2>
      <qrcode-scanner accept="application/pdf"
        :qrbox="250" 
        :fps="10" 
        style="width: auto"
        @result="onScan"
      />
      <a target="blank" :href="resultText"> {{resultText}}</a>
      <h2> Генерация QR-кода </h2>
      <QRCanvas :options="options"></QRCanvas>
      <br>
      <input v-model="text">
    </div>
  </div>
</template>

<script>
import QrcodeScanner from './components/QrcodeScanner.vue'
import {QRCanvas} from 'qrcanvas-vue'

export default {
  name: 'App',

  data: () => ({
    resultText: '',
    text: 'Ссылка'
  }), 

  components: {
    QrcodeScanner,
    QRCanvas 
  },

  computed: {
    options() {
      return {
        cellSize: 8,
        data: this.text,
      };
    },
  },

  methods: {
    onScan (decodedText, decodedResult) {
      console.log(decodedText, decodedResult)
      this.resultText=decodedText
    }
  }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

#first {
  width: auto;
  margin: 2%;
  background-color: #d8eefb;
  box-shadow: 7px 7px #489df2;
  padding: 25px;
  border-radius: 25px;
  position: relative;
  float: left;
}

</style>