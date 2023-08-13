<template>
  <div>
    <h3>{{ text.APP_NAME }}</h3>
  </div>
</template>

<script>
import TextConstant from "../assets/text.constant";
export default {
  name: "FundListing",
  data() {
    return {
      text: TextConstant,
    };
  },
};
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
  color: brown;
}
</style>
