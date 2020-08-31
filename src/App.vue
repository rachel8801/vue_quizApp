<template>
  <div id="app">
    <Header />

    <div class="quiz-box">
      <h2>Quiz-1 Computer Science Basic</h2>

      <div class="result" v-show="score_show">
        <p id="result1">Results</p>
        <p>You got {{score}}/{{questions.length}} questions correct!</p>
        <span id="percentage">{{finalResult}} %</span>
      </div>
      <form class="quiz-form" @submit.prevent="changOnSubmit()">
        <div class="question-box" v-for="(quesItem, index) in questions" :key="index">
          <div class="question-title">
            <p>{{index+1}}. {{quesItem.question}}</p>
          </div>

          <div class="suggest-answers">
            <ul>
              <li v-for="(answer, index) in quesItem.suggestions" :key="index">
                <input
                  class="radio"
                  :name="quesItem.question"
                  type="radio"
                  value="option"
                  required
                  :class="check(answer)"
                  v-on:click="addScore(answer)"
                />
                <label for="option">{{answer.suggestion}}</label>
              </li>
            </ul>
          </div>
        </div>

        <input class="button" type="submit" value="Submit" @click="score_show = 'true'" />
      </form>
      <div class="foot-note">
        <span>Answer all questions before submitting. Unanswered questions are displayed in yellow.</span>
      </div>
    </div>
  </div>
</template>

<script>
import Header from "./components/layout/Header";

export default {
  name: "App",
  components: {
    Header,
  },
  data() {
    return {
      questions: [],
      select: false,
      score: 0,
      score_show: false,
      color: " ",
      selectAnswer: [],
    };
  },
  methods: {
    addScore(item) {
      this.select = true;
      if (item.correct) {
        this.selectAnswer.push(item);
        this.score += 1;
      } else if (!item.correct) {
        const noScore = 0;
        this.score = noScore;
      }
    },
    check(status) {
      if (status.correct) {
        return (this.color = "green");
      } else {
        return (this.color = "red");
      }
    },

    changeOnSubmit() {
      alert("Review is incomplete. Please fill out every field.");
    },
  },
  computed: {
    finalResult() {
      return (this.score / this.questions.length) * 100;
    },
  },

  mounted() {
    fetch("./quiz.json")
      .then((res) => res.json())
      .then((json) => {
        // console.log(json);
        this.questions = json.results;
      });
    (response) => {
      console.log("Error loading json:", response);
    };
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: "Poppins", sans-serif;
}
.quiz-box {
  position: absolute;
  background-color: #f4f4f4;
  padding: 10px;
  border-bottom: 1px solid #ccc;
  text-align: center;
  width: 100%;
}
.quiz-box .question-box {
  display: block;
  width: 80%;
  height: auto;
  padding: 25px;
  font-size: 20px;
  text-align: left;
  background-color: #fff;
  border-width: 3px;
  border-style: solid;
  border-color: rgba(75, 64, 64, 0.753);
  border-radius: 10px;
  margin: 25px auto;
}
.quiz-box .question-box.hover ul {
  border-color: green;
}

h2 {
  margin: 25px;
}
p {
  padding-bottom: 20px;
}

ul li {
  position: relative;
  list-style: none;
  line-height: 2;
  border: 1px solid #cdd2d2;
  margin-bottom: 10px;
  border-radius: 15px;
  cursor: pointer;
  padding-left: 10px;
}

ul li input.correct {
  border-color: rgb(211, 23, 23);
}

ul label {
  padding-left: 15px;
}

.suggest-answers {
  padding-left: 20px;
}

.quiz-box input.button {
  margin: 30px;
  background-color: #15b815;
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
.foot-note span {
  color: rgb(211, 23, 23);
  font-size: 18px;
}
#result1 {
  text-decoration: underline;
}
.result p {
  font-size: 20px;
}
#percentage {
  font-weight: 800;
  color: red;
}
.question-box.correct {
  border: 3px solid green;
}
.question-box.incorrect {
  border: 3px solid red;
}

@media only screen and (max-width: 600px) {
  .quiz-box .question-box {
    display: block;
    width: 100%;
  }
}
</style>
