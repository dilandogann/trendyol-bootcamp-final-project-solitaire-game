<template>
  <div>
    <template v-if="showFront">
        <v-row>
          <v-col cols="12">
            <img :src="image" />
          </v-col>
        </v-row>
    </template>
    <template v-else>
      <v-row>
        <v-col cols="12">
          <img class="card-image" src="./../assets/hearts-back.jpg" />
        </v-col>
      </v-row>
    </template>
  </div>
</template>

<script>
export default {
  name: "PlayingCard",
  props: ["cardValue", "image", "showFront"],
  data() {
    return {
      oneLetterValues: [2, 3, 4, 5, 6, 7, 8, 9],
    };
  },
  computed: {
    flatValueClass() {
      return this.oneLetterValues.includes(this.cardValue)
        ? "one-letter-flat-value card-value"
        : "card-value";
    },
    rotatedValueClass() {
      return this.oneLetterValues.includes(this.cardValue)
        ? "one-letter-rotated-value card-value rotate"
        : "card-value rotate";
    },
  },
};
</script>

<style>
.card-image{
  border-radius: 8px;
}
</style>