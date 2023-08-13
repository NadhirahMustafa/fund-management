<template>
  <LandingPage pageTitle="Page title here"/>  
  <FundListing />
  <HistoryDetails />
</template>

<script>
import LandingPage from './pages/LandingPage.vue'
import FundListing from './pages/FundListing.vue'
// import HistoryDetails from './components/HistoryDetails.vue'

export default {
  name: 'App',
  components: {
    LandingPage,
    FundListing,
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