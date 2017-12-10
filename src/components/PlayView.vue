<template>
  <div class="o-vertical-fill tile is-vertical is-ancestor">
    <div class="o-vertical-fill__item o-vertical-fill__item--fixed tile is-parent">
      <div class="is-child tile box">
        <div class="has-text-centered">
          <h1 class="title">Currently won: <strong>{{ cash }}</strong></h1>
          <h2 class="subtitle">Round {{currentRound + 1}} of {{questions.length}}</h2>
        </div>
      </div>
    </div>
    <div class="o-vertical-fill__item tile">
      <div class="tile is-parent is-9">
        <div class="is-child tile">
          <game class="box" :question="currentQuestion"></game>
        </div>
      </div>
      <div class="tile is-parent">
        <div class="is-child tile box">
          <questions-bar :questions="questions"></questions-bar>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import QuestionsBar from './QuestionsBar.vue'
import exampleQuestions from '../common/exampleQuestions.json'
import Game from './Game.vue'
import {DIFFICULTY_LEVELS, STATUSES, REWARDS} from '../common/const.js'

export default {
  name: 'playView',

  components: {QuestionsBar, Game},
  data: function() {
    return {
      cash: 0,
      currentRound: 0,
      exampleQuestions
    }
  },
  computed: {
    currentQuestion: function() {
      return this.questions[this.currentRound]
    },
    maxRounds: function() {
    },
    questions: function() {
      return this.exampleQuestions.map((question,index) => ({
        ...question, 
        reward: REWARDS[index],
        isAnswered: index < this.currentRound
      })
      )
    }

  }
  
}
</script>


<style lang="scss">

  // styles for animations

  .flip-enter-active, .flip-leave-active {
    transition: all 0.5s linear;
  }
  .flip-enter, .flip-leave-to {
    transform: rotateY(90deg) scale(0.5, 1);
  }
</style>
