<template>
  <div class="question-box-container">
    <b-jumbotron>
      <template slot="lead">
        {{currentQuestion.question}}
      </template>
      <b-list-group>
        <b-list-group-item
          v-for="(answer, index) of answers" 
          :key="index"
          @click="selectAnwser(index)"
          :class="[selectedIndex === index ? 'selected' : '']"
        >
          {{ answer }}
        </b-list-group-item>
      </b-list-group>
      <b-button variant="primary" href="#">submit</b-button>&nbsp;
      <b-button @click="next" variant="success" href="#">Next</b-button>
    </b-jumbotron>
  </div>
</template>

<script>
export default {
  props: {
    currentQuestion: Object,
    next: Function
  },
  data() {
    return {
      selectedIndex: null
    }
  },
  computed: {
    answers() {
      let answers = [...this.currentQuestion.incorrect_answers]
      answers.push(this.currentQuestion.correct_answer)
      return answers
    } 
  },
  methods: {
    selectAnwser(index){
      this.selectedIndex = index
    }
  },
  mounted() {
    console.log(this.currentQuestion)
  }
}
</script>

<style scoped>
  .list-group {
    margin-bottom: 15px;
  }

  .list-group-item:hover {
    background: #EEE;
    cursor: pointer;
    color: red;
  }

  .btn {
    margin: 0 5px;
  }

  .selected {
    background-color: lightyellow;
  }

  .correct {
    background-color: lightgreen;
  }

  .incorect {
    background-color: red;
  }
</style>