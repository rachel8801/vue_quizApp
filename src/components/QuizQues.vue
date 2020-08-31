<template>
  <div class="question-boxes">
    <h2>Quiz-1 Computer Science Basic</h2>
    <div class="question-box" v-for="queList in quizQuestion" :key="queList.question">
      <p>{{queList.question}}</p>

      <span v-for="answer in answers" :key="answer">{{answer}}</span>
      <p>{{a}}</p>
    </div>
    <input class="button" type="submit" value="Submit" />
  </div>
</template>

<script>
export default {
  name: "QuizQues",
  props: {
    quizQuestion: {
      type: Array,
    },
  },

  data() {
    return {
      selectedIndex: null,
      correctIndex: null,
      answers: [1, 2],
    };
  },
  methods: {
    // selectedAnswer(index) {
    //   this.selectedIndex = index;
    // },
    shuffleAnswers() {
      // let a = [this.quizQuestion.incorrect_answers];
      // a.push(this.quizQuestion.correct_answer);
      // return (this.anwers = a);
      console.log(this.answers);
      // for (let i = 0; i < answers.length; i++) {
      //   let rand = Math.floor(Math.random() * answers.length);
      //   [answers[i], answers[rand]] = [answers[rand], answers[i]];
      // }
      // console.log(123);
      //  = answers;
    },
  },
  computed: {
    a() {
      return this.answers + " " + this.quizQuestion.correct_answer;
    },
  },
};
</script>

<style scoped>
.question-boxes {
  background-color: #f4f4f4;
  padding: 10px;
  border-bottom: 1px solid #ccc;
  text-align: center;
  width: 100%;
}
.question-boxes .question-box {
  display: block;
  width: 80%;
  height: auto;
  padding: 15px;
  font-size: 20px;
  text-align: left;
  border: 3px solid #cccccc;
  border-radius: 10px;
  margin: 25px auto;
}
h2 {
  margin: 25px;
}
p {
  padding-bottom: 15px;
}
span {
  padding-left: 18px;
}
.button {
  margin: 30px;
  background-color: #39495c;
  border-radius: 5px;
  font-size: 18px;
  width: 150px;
  height: 60px;
  color: white;
  padding: 20px;
  box-shadow: inset 0 -0.6em 1em -0.35em rgba(0, 0, 0, 0.17),
    inset 0 0.6em 2em -0.3em rgba(255, 255, 255, 0.15),
    inset 0 0 0em 0.05em rgba(255, 255, 255, 0.12);
  text-align: center;
  cursor: pointer;
}
</style>