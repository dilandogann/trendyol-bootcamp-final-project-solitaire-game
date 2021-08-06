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
          <p class="card-value">{{ cardValue }}</p>
          <img class="small-image" :src="smallImageUrl" />
        </div>
      </v-col>
      <v-col cols="8" class="custom-col">
        <img class="center-image" :src="centerImage" />
      </v-col>
      <v-col cols="2" class="custom-col">
        <div class="bottom-row-container">
          <img class="small-image rotate" :src="smallImage" />
          <p class="card-value rotate">{{ cardValue }}</p>
        </div>
      </v-col>
    </v-row>
  </v-card>
</template>

<script>
export default {
  name: "Card",
  props: ["cardValue", "smallImage", "centerImage"],
  data() {
    return {
      smallImageUrl: "",
    };
  },
  watch: {
    smallImage: {
      handler(val) {
        this.smallImageUrl = `'./../assets/'${val}`;
      },
      deep: true,
    },
  },
};
</script>

<style>
.main-card {
  height: fit-content;
  margin-top: 100px;
  width: 150px;
}
.card-value {
  font-size: 24px;
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
</style>