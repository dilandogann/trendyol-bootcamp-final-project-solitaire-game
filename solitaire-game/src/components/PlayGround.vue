<template>
  <v-row>
    <v-col v-for="(card,index) in cards" :key="index">
      <playing-card :cardValue="card.value" :image="card.image" :showFront="card.showFront"/>
    </v-col>
  </v-row>
</template>

<script>
import PlayingCard from "../components/PlayingCard.vue";
import cardValues from "../cardValues";
import Card from "../Card";

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
      for (let i = 0; i < 8; i++) {
        this.createPlayingCard();
      }
    },
    createPlayingCard() {
      const cards = this.cardValues.map((cardItem) => {
        return new Card(cardItem.value, cardItem.image);
      });
      this.cards.push(...cards);
    },
    initializeGame() {},
  },
};
</script>

<style>
</style>