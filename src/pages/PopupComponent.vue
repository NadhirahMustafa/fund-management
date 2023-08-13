<template>
  <div class="popup-overlay" @click="closePopup">
    <div class="popup-container" @click.stop>
      <h2>
        <div class="details-margin">
          <b>{{ dataJson.fundName }}</b>
        </div>
      </h2>
      <div class="details-margin">
        {{ dataJson.description }}
      </div>
      <div class="details-margin">
        {{ dataJson.currency }} {{ dataJson.fundSize }}
      </div>
      <div class="details-margin">
        {{ dataJson.investmentType }}
      </div>
      <div class="details-margin">
        {{ dataJson.shariahCompliance }}
      </div>
      <div class="details-margin">
        {{ dataJson.currency }} {{ dataJson.currentNAV }}
      </div>
      <div class="details-margin">
        {{ dataJson.riskRating }}
      </div>
      <div class="details-margin">
        {{ dataJson.SubscriptionStatus }}
      </div>
      <table>
        <thead>
          <tr>
            <th>Currency</th>
            <th>Ex-Date</th>
            <th>Reinvestment Date</th>
            <th>Payment Date</th>
            <th>Distribution</th>
            <th>Yield</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(data, index) in dataJson.HistoryData" :key="index">
            <td>{{ data.currency }}</td>
            <td>{{ data.exDate }}</td>
            <td>{{ data.reinvestmentDate }}</td>
            <td>{{ data.paymentDate }}</td>
            <td>{{ data.distribution }}</td>
            <td>{{ data.yield }}</td>
          </tr>
        </tbody>
      </table>
      <slot></slot>
      <button @click="closePopup">Close</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    id: Number,
    dataJson: {
      type: Object,
      default: () => {},
    },
  },
  methods: {
    closePopup() {
      this.$emit("close");
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
