<template>
  <div v-if="dataFetched">
    <div class="card-arr">
      <div v-for="fundList in fundListing" :key="fundList.id">
        <div class="card-grid">
          <div>
            <div class="details-margin">
              <b class="large-font">{{ fundList.fundName }}</b>
            </div>
            <div class="details-margin green-border">
              {{ fundList.investmentType }}
            </div>
            <div class="details-margin yellow-border">
              {{ fundList.shariahCompliance === 'Yes' ? constant.SHARIAH : constant.CONVENTIONAL }}
            </div>
            <div class="details-margin pink-border">
              <div><b>Current NAV</b></div>
              <div>
                {{ fundList.currency }} {{ fundList.currentNAV }}
              </div>
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
import FundConstant from '../assets/fund.constant'
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
      constant: FundConstant
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
.pink-border {
  border: 1px rgb(253, 0, 177) dotted;
  background-color: rgb(250, 131, 214);
}
.green-border {
  border: 1px green dotted;
  background-color: rgb(108, 248, 108);
}
.yellow-border {
  border: 1px rgb(255, 187, 0) dotted;
  background-color: rgb(253, 241, 209);
}
.large-font {
  font-size: larger;
}
.card-grid {
  width: 200px;
  height: 100%;
  margin: 10px 10px 10px 10px;
  border-radius: 2%;
  border: 1px rgb(173, 173, 173) ridge;
}
.card-arr {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
.card-highlight {
  border: 1px rgb(252, 0, 21) solid;
  background-color: rgb(248, 79, 79);
}
.details-margin {
  margin: 10px;
}
</style>
