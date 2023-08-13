<template>
  <div class="popup-overlay" @click="closePopup">
    <div class="popup-container" @click.stop>
      <h2>
        <div class="details-margin">
          <b>{{ dataJson.fundName }}</b>
        </div>
      </h2>
      <div class="details-margin">
        <div>Unit to purchase:</div>
        <input
          type="text"
          id="text-input"
          v-model="inputText"
          @input="handleUnitInput"
        />
      </div>
      <div class="details-margin">
        <div>Amount:</div>
        {{ totalPrice.toFixed(2) }}
      </div>
      <slot></slot>
      <button @click="closePopup">Add</button
      ><button @click="closePopup">Close</button>
    </div>
  </div>
</template>

<script>
import unitPrice from "../assets/unitPrice.json";
export default {
  name: "AddFund",
  data() {
    return {
      dataFetched: false,
      pricePerUnit: [],
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
      console.log("test: ", this.inputText, this.totalPrice, this.pricePerUnit);
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
</style>
