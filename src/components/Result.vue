<template>
  <div>
    <b-card class="mb-2 mx-auto shadow">
      <h2>{{ finalScores >= 3 ? "Contratulation!" : "oOps!" }}</h2>
      <p>You Answered</p>
      <h1>{{ finalScores }}/5</h1>

      <p>questions correct</p>

      <b-button @click="tryAgain" variant="success">Try Again</b-button>
    </b-card>
  </div>
</template>


<script>
export default {
  name: "Result",
  props: {
    finalScores: Number,
    showResult: Boolean,
  },
  methods: {
    tryAgain() {
      location.reload();
    },
  },
};
</script>


<style scoped>
.status {
  margin-top: -3rem;
}
h2 {
  font-family: "Do Hyeon", sans-serif;
  font-size: 40px;
  color: #ac3b61;
  font-weight: 900;
}
h1 {
  font-family: "Do Hyeon", sans-serif;
  font-size: 35px;
  color: #2ddaa5;
}
p {
  font-weight: 600;
  font-size: 18px;
}
.progress-bar {
  background-color: #f5f7f7 !important;
  flex-direction: row !important;
}
</style>