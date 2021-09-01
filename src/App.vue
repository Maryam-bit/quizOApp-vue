<template>
  <div id="app">
    <Header />
    <b-container class="bv-example-row mt-5 pt-5">
      <b-row class="text-center">
        <b-col></b-col>
        <b-col lg="8" md="12">
          <QuestionBox
            v-if="questions.length && !showResult"
            :currentQuestion="questions[index]"
            :next="next"
            :index="index"
            @totalScore="total"
          />
          <Loading v-else-if="!questions.length" />
          <Result
            v-show="showResult"
            :finalScores="finalScores"
            :showResult="showResult"
          />
        </b-col>
        <b-col></b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import QuestionBox from "./components/QuestionsBox.vue";
import Loading from "./components/Loading.vue";
import Result from "./components/Result.vue";
export default {
  name: "App",
  components: {
    Header,
    QuestionBox,
    Loading,
    Result,
  },
  
  data() {
    return {
      questions: [],
      index: 0,       // index of questions
      showResult: false,    // show result component based on condition
      finalScores: 0,
    };
  },

  methods: {
    next(picked) {
      this.index++;
      console.log(picked, "picked value from app");
      if (this.index > 4) {         // when all question complete then show result component
        this.showResult = true;
      }
    },
    total(val) {
      console.log(val, "value");
      this.finalScores += val;      // getting total scores from question component and passing into reult component
    },
  },

  mounted: function () {
    fetch("https://opentdb.com/api.php?amount=5&category=18&type=multiple", {
      method: "get",
    })
      .then((response) => {
        return response.json();
      })
      .then((jsonData) => {
        this.questions = jsonData.results;
      });
  },
};
</script>


<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background-color: #eeffe8;
  height: 100vh;
}
</style>
