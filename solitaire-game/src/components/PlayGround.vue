<template>
  <v-container>
    <v-row>
      <v-col cols="1"></v-col>
      <v-col
        v-for="(playingCardSuit,suitIndex) in playingCards"
        :key="suitIndex"
        >
        <v-row
          v-for="playingCard in playingCardSuit"
          :key="playingCard.id"
          >
          <playing-card
            :cardValue="playingCard.value"
            :image="playingCard.image"
            :showFront="playingCard.showFront"
          />
        </v-row>
      </v-col>
      <v-col cols="1"></v-col>
    </v-row>
  </v-container>
</template>

<script>
import _ from "lodash";

import PlayingCard from "../components/PlayingCard.vue";
import cardValues from "../cardValues";
import Card from "../Card";

export default {
  components: { PlayingCard },
  name: "PlayGround",
  data() {
    return {
      id: 1,
      cards: [],
      playingCards: [],
      floorCards: [],
    };
  },
  created() {
    this.cardValues = cardValues;
    this.initializeCards();
    this.shuffleCards();
    this.getRandomPlayGroundCards();
    this.getRemainingFloorCards();
    this.chunkPlayingCards();
  },
  methods: {
    //It creates 8 copy of each playing cards
    initializeCards() {
      for (let i = 0; i < 8; i++) {
        this.createPlayingCard();
      }
    },
    //It creates 13 playing cards
    createPlayingCard() {
      const cards = this.cardValues.map((cardItem) => {
        return new Card(cardItem.value, cardItem.image, this.id++);
      });
      this.cards.push(...cards);
    },
    //It randomly shuffles the cards array
    shuffleCards() {
      const shuffledCards = _.shuffle(this.cards);
      this.cards = shuffledCards;
    },
    //It randomly picks 54 cards for playing ground
    getRandomPlayGroundCards() {
      // lower and upper value
      let lower = 0;
      let upper = 103;

      let randomIndexes = [];

      // Calculating 54 random values in range 0 and 103
      while (this.playingCards.length !== 54) {
        let randomNum = _.random(lower, upper);
        if (randomIndexes.includes(randomNum)) continue;
        this.playingCards.push(this.cards[randomNum]);
        randomIndexes.push(randomNum);
      }
    },
    getRemainingFloorCards() {
      //Get remaining cards for floorCards
      this.floorCards = this.cards.filter((card) => {
        let filtered = this.playingCards.filter(
          (playCard) => playCard.id === card.id
        );
        if (filtered.length === 0) return card;
      });
    },
    chunkPlayingCards() {
      const overflowingItems = this.playingCards.slice(-4);
      this.playingCards = this.playingCards.slice(
        0,
        this.playingCards.length - 4
      );
      this.playingCards = _.chunk(this.playingCards, 5);
      for (let i = 0; i < overflowingItems.length; i++) {
        this.playingCards[i].push(overflowingItems[i]);
      }
    },
    initializeGame() {},
    calculateLength(val) {
      console.log(val);
      return val.size;
    },
  },
};
</script>

<style>
</style>