<template>
  <LandingPage pageTitle="Page title here"/>  
  <FundDetails />
  <HistoryDetails />
</template>

<script>
import LandingPage from './components/LandingPage.vue'
import FundDetails from './components/FundDetails.vue'
// import HistoryDetails from './components/HistoryDetails.vue'

export default {
  name: 'App',
  components: {
    LandingPage,
    FundDetails
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
</style>
