<template>
  <div class="card-arr">
    <div v-for="fundList in fundListing" :key="fundList.id">
      <div class="card-grid">
        <div>
          <button
            style="background-color: transparent; border: none"
            @click="handleFundDetails(fundList)"
          >
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
          </button>

          <div>
            <PopupComponent
              v-if="isPopupVisible"
              @close="closePopup"
              :id="isSelectedId"
              :dataJson="isSelectedDetails"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import fundData from "../assets/fundList.json";
import PopupComponent from "./PopupComponent.vue";
export default {
  name: "FundListing",
  data() {
    return {
      fundListing: fundData,
      showModal: false,
      isPopupVisible: false,
      isSelectedId: 0,
      isSelectedDetails: null
    };
  },
  components: {
    PopupComponent,
  },
  methods: {
    handleFundDetails(fundList) {
      console.log("button triggered");
      this.isSelectedId = fundList.id;
      this.isSelectedDetails = fundList;
      this.isPopupVisible = true;
    },
    showPopup() {
      this.isPopupVisible = true;
    },
    closePopup() {
      this.isPopupVisible = false;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
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
