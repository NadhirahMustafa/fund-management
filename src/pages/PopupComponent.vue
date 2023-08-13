<template>
  <div class="popup-overlay" @click="closePopup">
    <div class="popup-container" @click.stop>
      <h2>
        <div class="details-margin popup-title">
          <b>{{ dataJson.fundName }}</b>
        </div>
      </h2>
      <div class="divider" />
      <div>
        <div class="details-margin">
          {{ dataJson.description }}
        </div>
        <div class="details-arr details-margin">
          <div class="label">Fund size:</div>
          <div>{{ dataJson.currency }} {{ dataJson.fundSize }}</div>
        </div>
        <div class="details-arr details-margin">
          <div class="label">Investment Type:</div>
          <div>
            {{ dataJson.investmentType }}
          </div>
        </div>
        <div class="details-arr details-margin">
          <div class="label">Shariah Compliance:</div>
          <div>
            {{ dataJson.shariahCompliance }}
          </div>
        </div>
        <div class="details-arr details-margin">
          <div class="label">Current NAV:</div>
          <div>{{ dataJson.currency }} {{ dataJson.currentNAV }}</div>
        </div>
        <div class="details-arr details-margin">
          <div class="label">Risk Rating:</div>
          <div>
            {{ dataJson.RiskRating }}
          </div>
        </div>
        <div class="details-arr details-margin">
          <div class="label">Subscription Status:</div>
          <div>
            {{ dataJson.SubscriptionStatus }}
          </div>
        </div>
      </div>
      <div class="divider" />
      <div class="details-arr details-margin">
        <div class="table-title">Funds History</div>
      </div>
      <table class="table-margin">
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
.table-margin {
  margin-bottom: 30px;
}
.divider {
  border-top: 1px black solid;
}
.table-title {
  justify-content: center;
  font-weight: bold;
  margin-top: 10px;
}
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
.popup-title {
  font-size: larger;
  color: brown;
}
.details-margin {
  margin: 10px;
}
.label {
  margin-right: 5px;
  font-weight: bold;
}
.details-arr {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
.table {
  margin-right: 20px;
  border: 1px red solid;
}
th {
  padding-right: 10px;
  justify-content: center;
  justify-items: center;
}
td {
  padding-right: 10px;
}
</style>
