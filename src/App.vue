<template>
  <div id="app">
    <InvoiceDetail 
      :invoice="{
        inv_date: new Date(),
        inv_template: '01GTGT',
        inv_seri: 'BT/19P',
        inv_no: '000126',
        items: [{no: 1},{no: 2},{no: 3},{no:4},{no:5}]
      }"
    ></InvoiceDetail>
  </div>
</template>

<script>
import InvoiceDetail from './components/InvoiceDetail.vue'
export default {
  name: 'App',
  components: {
    InvoiceDetail
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
*{
  font-family: TimeNewRoman;
}
@font-face {
  font-family: TimeNewRoman;
  src: url('./assets/Fonts/font-times-new-roman/SVN-Times\ New\ Roman.ttf');
}
@font-face {
  font-family: TimeNewRomanBold;
  src: url('./assets/Fonts/font-times-new-roman/SVN-Times\ New\ Roman\ 2\ bold.ttf');
}

</style>
