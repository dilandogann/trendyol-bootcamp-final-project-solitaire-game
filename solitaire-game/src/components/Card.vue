<template>
  <v-card
    class="main-card d-flex align-stretch mb-6"
    color="grey lighten-2"
    flat
    tile
  >
    <div class="row">
      <div class="col-sm-3 card-header-footer">
        <div class="rank">K</div>
        <div class="rank small"></div>
      </div>
      <div class="col-sm-6">
        <v-img
          class="white--text align-end"
          height="130px"
          weight="80px"
          src="./../assets/maca-buyuk.webp"
        >
        </v-img>
      </div>
      <div class="col-sm-3 card-header-footer">
        <div>K</div>
        <div>
          <v-img
            class="white--text align-end"
            height="10px"
            weight="10px"
            src="./../assets/maca-min.png"
          >
          </v-img>
        </div>
      </div>
    </div>
  </v-card>
</template>

<script>
export default {
  name: "Card",
};
</script>

<style>
.main-card {
  width: 134px;
  height: 210px;
}
.card-header-footer {
  height: 40px;
}
.card-middle {
  height: 130px;
}
.small{
    background-image: url('./../assets/maca-min.png')
}
</style>