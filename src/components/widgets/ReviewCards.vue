<template>
  <div>
    <v-row>
      <v-col v-for="n in 3" :key="n">
        <v-card
          class="mx-auto card-class"
          color="#ffffff"
          style="border-radius: 15px; margin: 4%"
          max-width="500"
          max-height="200"
          min-height="200"
          min-width="350"
        >
          <v-card-title v-if="n == 1">
            <v-icon large left> mdi-chart-bar </v-icon>
            <span class="text-h6 font-weight-light text"> Total Reviews</span>
          </v-card-title>
          <v-card-title v-if="n == 2">
            <v-icon large left> mdi-chart-bar </v-icon>
            <span class="text-h6 font-weight-light text">Review Stats</span>
          </v-card-title>
          <v-card-title v-if="n == 3">
            <v-icon large left> mdi-chart-bar </v-icon>
            <span class="text-h6 font-weight-light text">Review health</span>
          </v-card-title>

          <v-card-text
            class="font-weight-bold text"
            style="padding-left: 5%"
            v-if="n == 2"
          >
            <v-row
              v-for="(reviewitem, index) in reviewFilterData"
              :key="reviewitem[index]"
            >
              <v-rating
                readonly
                background-color="purple lighten-3"
                :value="parseInt(index)"
                color="#e75480"
                x-small
              >
              </v-rating>
              <v-spacer></v-spacer>
              <b style="padding-right:10px" class="text"> {{ reviewitem }}</b>
            </v-row>
          </v-card-text>

          <v-card-actions>
            <v-list-item class="grow">
              <v-list-item-avatar v-if="n == 1" color="grey darken-3">
                <v-img
                  class="elevation-6"
                  alt=""
                  src="https://avataaars.io/?avatarStyle=Transparent&topType=ShortHairShortCurly&accessoriesType=Prescription02&hairColor=Black&facialHairType=Blank&clotheType=Hoodie&clotheColor=White&eyeType=Default&eyebrowType=DefaultNatural&mouthType=Default&skinColor=Light"
                ></v-img>
              </v-list-item-avatar>
              <v-list-item-content>
                <v-list-item-title v-if="n == 1" class="text"
                  >Total Reviews</v-list-item-title
                >
                <v-list-item-title v-if="n == 3" class="text">
                  Current Status</v-list-item-title
                >
              </v-list-item-content>
              <span class="subheading" v-if="n == 1">
                <b class="text"> {{ reviewData && reviewData.length }}</b>
              </span>
              <span class="subheading" v-if="n == 2"> </span>
              <span class="subheading" v-if="n == 3">
                <v-chip dark :color="healthText.color" class="text">
                  <v-icon dark>
                    {{ healthText.color }} {{ healthText.icon }}</v-icon
                  >
                  {{ healthText.text }}</v-chip
                >
              </span>
            </v-list-item>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>
<script>
import reviewData from "@/assets/reviewData.json";

export default {
  name: "ReviewCards",
  data() {
    return {
      reviewFilterData: [],
      reviewData: reviewData,
      healthText: {
        text: "Awesome",
        icon: "mdi-star-outline",
        color: "#006400",
      },
    };
  },
  /**
   * To set before rendering of page
   */
  beforeMount() {
    this.filtercardData();
  },
  methods: {
    /**
     * @method filtercardData filtering data from provided json to fetch
     * count of all distinct rating reviews Eg 1,2,3,4,5 & respective count
     * If any new rating introduced measure added no method change will be required
     */
    filtercardData() {
      let overallUniqueValues = [];
      overallUniqueValues = reviewData.reduce((acc, val) => {
        acc[val.overall] =
          acc[val.overall] === undefined ? 1 : (acc[val.overall] += 1);
        return acc;
      }, {});
      this.reviewFilterData = overallUniqueValues;
      this.getReviewHealthStats();
    },
    /**
     * @method getReviewHealthStats - this method provide current health status
     * based on health status return text,color & icon
     * Overall - Finds Largest no in overall unique stats
     */
    getReviewHealthStats() {
      let overall = Object.keys(this.reviewFilterData).reduce((a, b) =>
        this.reviewFilterData[a] > this.reviewFilterData[b] ? a : b
      );
      if (this.reviewFilterData && this.reviewFilterData.length && overall) {
        console.log(overall);
        if (overall === "5") {
          return (this.healthText = {
            text: "Awesome",
            icon: "mdi-star-outline",
            color: "#006400",
          });
        } else if (overall === "4") {
          return (this.healthText = {
            text: "Good",
            icon: "mdi-marker-check",
            color: "#90ee90",
          });
        } else if (overall === "3") {
          return (this.healthText = {
            text: "Average",
            icon: "mdi-alert-circle-outline",
            color: "#9b870c",
          });
        } else if (overall === "2") {
          return (this.healthText = {
            text: "Below Avg",
            icon: "mdi-alert-octagram",
            color: "#FFFF00",
          });
        } else {
          return (this.healthText = {
            text: "Poor",
            icon: "mdi-close-circle-outline",
            color: "#8B0000",
          });
        }
      }
    },
  },
};
</script>
<style scoped>
.card-class {
  color: #363472;
}
.text {
  font-family: Roboto;
  color: #363472;
}
</style>

