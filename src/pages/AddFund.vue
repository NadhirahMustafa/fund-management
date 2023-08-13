<template>
  <div class="popup-overlay" @click="closePopup">
    <div class="popup-container" @click.stop>
      <h2>
        <div class="details-margin popup-title">
          <b>{{ dataJson.fundName }}</b>
        </div>
      </h2>
      <div class="divider" />
      <div class="details-arr details-margin">
        <div class="label">{{ text.UNIT_TO_PURCHASE }}</div>
        <input
          type="text"
          id="text-input"
          v-model="inputText"
          @input="handleUnitInput"
        />
      </div>
      <div class="divider" />
      <div class="details-arr details-margin">
        <div class="label">{{ text.AMOUNT }}</div>
        <div>{{ totalPrice.toFixed(2) }}</div>
      </div>

      <div class="divider" />
      <button class="button-margin" @click="closePopup">
        {{ text.PROCEED_TO_PAYMENT }}</button
      ><button @click="closePopup">{{ text.CANCEL }}</button>
    </div>
  </div>
</template>

<script>
import TextConstant from "../assets/text.constant";
import unitPrice from "../assets/unitPrice.json";
export default {
  name: "AddFund",
  data() {
    return {
      dataFetched: false,
      pricePerUnit: [],
      text: TextConstant,
      totalPrice: 0,
    };
  },
  props: {
    id: Number,
    dataJson: {
      type: Object,
      default: () => {},
    },
  },
  mounted() {
    this.fetchData();
  },
  methods: {
    fetchData() {
      setTimeout(() => {
        this.pricePerUnit = unitPrice;
        this.dataFetched = true;
      }, 1000);
    },
    closePopup() {
      this.$emit("close");
    },
    handleUnitInput(event) {
      this.inputText = event.target.value;
      this.totalPrice =
        Number(this.inputText) * Number(this.pricePerUnit.unitPrice);
    },
  },
};
</script>

<style scoped>
.popup-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.popup-container {
  background-color: white;
  padding: 20px;
  border-radius: 5px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}
.details-margin {
  margin: 10px;
}
.details-arr {
  display: flex;
  flex-wrap: wrap;
  margin: 10px;
}

.popup-title {
  font-size: larger;
  color: brown;
}
.divider {
  border-top: 1px black solid;
}
.label {
  margin-right: 5px;
  font-weight: bold;
}
.button-margin {
  margin: 10px;
}
</style>
