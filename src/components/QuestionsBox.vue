<template>
    <div>
      <b-card
        :title="currentQuestion.question"
        img-alt="Image"
        img-top
        tag="article"
        class="mx-auto shadow question bg-light p-5"
      >
        <div v-for="(answer, index) in shuffledAnswers" :key="index">
          <label>
            <input
              type="radio"
              :value="answer"
              :name="answer"
              v-model="picked"
            />
            {{ answer }}
          </label>
          <br />
        </div>
        <b-button
          :disabled="!picked"
          @click="
            next(picked);
            handleNext();
          "
          href="#"
          variant="success"
          class="m-3"
          >Next</b-button
        >
      </b-card>
    </div>
</template>


<script>
import _ from "lodash";
export default {
  name: "QuestionBox",
  props: {
    currentQuestion: Object,
    next: Function,
    index: Number,
  },
  data() {
    return {
      shuffledAnswers: [],
      picked: "",
      score: 0,
    };
  },
  watch: {
    currentQuestion: {    
      immediate: true,
      handler() {
        this.picked = "";           
        this.shuffleAnswers();
      },
    },
  },
  methods: {
    handleNext() {
      console.log(
        this.picked === this.currentQuestion.correct_answer ? "true" : "false"
      );
      if (this.picked === this.currentQuestion.correct_answer) {
        this.score += 1;
      }
      console.log(this.index);
      if (this.index >= 4) {
        this.$emit("totalScore", this.score);
      }
    },
    shuffleAnswers() {
      let answer = [
        ...this.currentQuestion.incorrect_answers,
        this.currentQuestion.correct_answer,
      ];
      this.shuffledAnswers = _.shuffle(answer);
    },
  },
};
</script>


<style scoped>
.question {
  color: #637368;
}
.list-group-item:hover {
  background-color: #eee;
  cursor: pointer;
}
</style>