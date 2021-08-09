<template>
  <v-container style="margin-top: 100px">
    <v-row>
      <v-col cols="1"></v-col>
      <v-col
        v-for="(playingCardSuit, suitIndex) in playingCards"
        :key="suitIndex"
      >
        <draggable
          :list="playingCardSuit"
          :move="checkMove"
          draggable=".js-draggable-file-list-item"
          animation="200"
        >
          <v-row v-for="playingCard in playingCardSuit" :key="playingCard.id">
            <playing-card
              :draggable="playingCard.showFront"
              :class="
                playingCard.showFront
                  ? 'js-draggable-file-list-item cursor playingCard'
                  : 'playingCard'
              "
              :card="playingCard"
              animation="200"
            />
          </v-row>
        </draggable>
      </v-col>
      <v-col cols="1"></v-col>
    </v-row>
    <div
      class="floorCards cursor"
      v-for="card in floorCards"
      :key="card.id"
      @click="dealFloorCards"
    >
      <playing-card :card="card"> </playing-card>
    </div>
  </v-container>
</template>

<script>
import draggable from "vuedraggable";
import _ from "lodash";
import PlayingCard from "../components/PlayingCard.vue";
import cardValues from "../cardValues";
import Card from "../Card";

export default {
  components: { PlayingCard, draggable },
  name: "PlayGround",
  data() {
    return {
      index: 1,
      id: 1,
      cards: [],
      playingCards: [],
      floorCards: [],
    };
  },
  created() {
    this.initializeGame();
  },
  methods: {
    initializeGame() {
      this.initializeCards();
      this.shuffleCards();
      this.getRandomPlayGroundCards();
      this.getRemainingFloorCards();
      this.chunkPlayingCards();
      this.showFrontSideOfLastCardsInChunks();
    },
    //It creates 8 copy of each playing cards
    initializeCards() {
      for (let i = 0; i < 8; i++) {
        this.createPlayingCard();
      }
    },
    //It creates 13 playing cards
    createPlayingCard() {
      const cards = cardValues.map((cardItem) => {
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
      // lower and upper bounds
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
    //Get remaining cards for floorCards
    getRemainingFloorCards() {
      this.floorCards = this.cards.filter((card) => {
        let filtered = this.playingCards.filter(
          (playCard) => playCard.id === card.id
        );
        if (filtered.length === 0) return card;
      });
    },
    //Creating 6-6-6-6-5-5-5-5-5-5 chunks of playingCards array
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
    //It changes last card's of chunks showFront property in order to showing front side
    showFrontSideOfLastCardsInChunks() {
      for (let i = 0; i < this.playingCards.length; i++) {
        const length = this.playingCards[i].length;
        this.playingCards[i][length - 1].showFront = true;
      }
    },
    checkMove: function (evt) {
      return evt.draggedContext.element.showFront;
    },
    //When user clicks deal one card to each shuffle
    dealFloorCards() {
      for (let i = 0; i < 10; i++) {
        const card = this.floorCards.shift();
        card.showFront = true;
        this.playingCards[i].push(card);
      }
    },
    //It makes last card of given chunk visible 
    showLastElementWhenAllChunkIsReversed(chunkIndex){
      const chunkLength=this.playingCards[chunkIndex].length;
      const lastCardOfChunk=this.playingCards[chunkIndex][chunkLength-1]
        if(!lastCardOfChunk.showFront)
          lastCardOfChunk.showFront=true
    }
  },
};
</script>

<style>
.cursor{
    cursor: pointer;
}
.playingCard {
  margin-bottom: -4.5vw;
}
.floorCards {
  position: absolute;
  right: 30px;
  bottom: 30px;
}
</style>