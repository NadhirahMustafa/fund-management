<template>
  <div v-if="dataFetched">
    <div class="card-arr">
      <div v-for="fundList in fundListing" :key="fundList.id">
        <div class="card-grid">
          <div>
            <div class="details-margin">
              <b>{{ fundList.fundName }}</b>
            </div>
            <div class="details-margin">
              {{ fundList.description }}
            </div>
            <div class="details-margin">
              {{ fundList.investmentType }}
            </div>
            <div class="details-margin">
              {{ fundList.shariahCompliance }}
            </div>
            <div class="details-margin">
              {{ fundList.currency }} {{ fundList.currentNAV }}
            </div>
            <button
              style="background-color: transparent; border: none"
              @click="handleFundDetails(fundList)"
            >
              View Details
            </button>
            <button
              style="background-color: transparent; border: none"
              @click="handleAddFund(fundList)"
            >
              Add Amount
            </button>

            <div>
              <PopupComponent
                v-if="isPopupVisible"
                @close="closePopup"
                :id="isSelectedId"
                :dataJson="isSelectedDetails"
              />
            </div>
            <div>
              <AddFund
                v-if="isPopupAddVisible"
                @close="closePopup"
                :id="isSelectedId"
                :dataJson="isSelectedDetails"
              />
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import fundData from "../assets/fundList.json";
import PopupComponent from "./PopupComponent.vue";
import AddFund from "./AddFund.vue";
export default {
  name: "FundListing",
  data() {
    return {
      dataFetched: false,
      fundListing: [],
      showModal: false,
      isPopupVisible: false,
      isSelectedId: 0,
      isSelectedDetails: null,
      isPopupAddVisible: false,
    };
  },
  components: {
    PopupComponent,
    AddFund,
  },
  mounted() {
    this.fetchData();
  },
  methods: {
    fetchData() {
      setTimeout(() => {
        this.fundListing = fundData;
        this.dataFetched = true;
      }, 1000);
    },
    handleFundDetails(fundList) {
      this.isSelectedId = fundList.id;
      this.isSelectedDetails = fundList;
      this.isPopupVisible = true;
    },
    showPopup() {
      this.isPopupVisible = true;
    },
    closePopup() {
      this.isPopupVisible = false;
      this.isPopupAddVisible = false;
    },
    handleAddFund(fundList) {
      this.isSelectedId = fundList.id;
      this.isSelectedDetails = fundList;
      this.isPopupAddVisible = true;
    },
  },
};
</script>

<style scoped>
.card-grid {
  width: 200px;
  height: 100%;
  font-size: 20px;
  padding: 10px 8px 10px 8px;
}
.card-arr {
  display: flex;
  flex-wrap: wrap;
}
.card-highlight {
  border: 1px rgb(252, 0, 21) solid;
  background-color: rgb(248, 79, 79);
}
.details-margin {
  margin: 10px;
}
</style>
