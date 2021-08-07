<template>
  <v-row>
    <v-col v-for="card in cards" :key="card.value">
        <playing-card :cardValue="card.value" :centerImage="card.centerImg" />
    </v-col>
  </v-row>
</template>

<script>
import PlayingCard from "../components/PlayingCard.vue";
import cardValues from "../cardValues";
import Card from "../Card"

export default {
  components: { PlayingCard },
  name: "PlayGround",
  data() {
    return {
      cards: [],
    };
  },
  created() {
    this.cardValues = cardValues;
    this.initializeCards();
  },
  methods: {
    initializeCards() {
      this.cards=this.cardValues.map((cardItem) => {
        return new Card(cardItem.value,cardItem.centerImage);
      });
    },
    initializeGame() {},
  },
};
</script>

<style>
</style>