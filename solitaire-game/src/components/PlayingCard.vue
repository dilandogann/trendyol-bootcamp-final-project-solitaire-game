<template>
  <v-card
    class="main-card d-flex align-stretch"
    color="grey lighten-2"
    flat
    tile
  >
    <v-row class="custom-row">
      <v-col cols="2" class="custom-col">
        <div class="top-row-container">
          <p :class="flatValueClass">{{ cardValue }}</p>
          <img class="small-image" src="./../assets/spades-min.png" />
        </div>
      </v-col>
      <v-col cols="8" class="custom-col">
        <img class="center-image" :src="centerImage" />
      </v-col>
      <v-col cols="2" class="custom-col">
        <div class="bottom-row-container">
          <img class="small-image rotate" src="./../assets/spades-min.png" />
          <p :class="rotatedValueClass">{{ cardValue }}</p>
        </div>
      </v-col>
    </v-row>
  </v-card>
</template>

<script>
export default {
  name: "PlayingCard",
  props: ["cardValue",  "centerImage"],
  data() {
    return {
      oneLetterValues:[2,3,4,5,6,7,8,9]
    };
  },
  computed:{
    flatValueClass(){
      return this.oneLetterValues.includes(this.cardValue) ? "one-letter-flat-value card-value" : "card-value"
    },
    rotatedValueClass(){
      return this.oneLetterValues.includes(this.cardValue) ? "one-letter-rotated-value card-value rotate" : "card-value rotate"
    }
  }
};
</script>

<style>
.main-card {
  height: fit-content;
  margin-top: 100px;
  width: 150px;
}
.card-value {
  font-size: 20px;
  font-weight:600;
}
.custom-row {
  margin: 0 !important;
}
.custom-col {
  padding: 0 !important;
}
.bottom-row-container {
  position: absolute;
  bottom: 6px;
  right: 4px;
  line-height: 18px;
}
.top-row-container {
  position: absolute;
  top: 2px;
  left: 4px;
  line-height: 22px;
}
.small-image {
  height: 20px;
}
.center-image {
  margin-top: 20px;
  margin-bottom: 20px;
  height: 160px;
  width: 100px;
}
.rotate {
  transform: rotate(180deg);
}
.one-letter-flat-value{
  margin-left: 4px;
}
.one-letter-rotated-value{
  margin-right: 4px;
}
</style>