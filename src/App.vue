<template>
  <div class="container-app">
    <div class="container-quiz">
      <div class="header-quiz">
        <h1>Quiz App</h1>
      </div>
      <div class="step-progress" :style="{ width: progress + '%' }"></div>
      <div
        class="box"
        v-for="(question, index) in questions.slice(a, b)"
        :key="index"
        v-show="quiz"
      >
        <div class="box-question">
          <h2>Question {{ b }}/{{ questions.length }}</h2>
          <p>{{ question.question }}</p>
        </div>
        <div class="box-propositions">
          <ul>
            <li
              v-for="(proposition, index) in question.propositions"
              :key="index"
              class="li"
              @click="selectResponse(proposition, index)"
              :class="correct ? check(proposition) : ''"
            >
              {{ proposition.props }}
              <div
                class="fas fa-check"
                v-if="correct ? proposition.correct : ''"
              ></div>
              <div
                class="fas fa-times"
                v-if="correct ? !proposition.correct : ''"
              ></div>
            </li>
          </ul>
        </div>
      </div>
      <div class="box-score" v-if="score_show">
        <h2>Your score is</h2>
        <h2>{{ score }}/{{ questions.length }}</h2>
        <div class="btn-restart">
          <button @click="restartQuiz">
            Restart <i class="fas fa-sync-alt"></i>
          </button>
        </div>
      </div>
      <div class="footer-quiz">
        <div v-if="progress < 100" class="box-button">
          <button
            @click="skipQuestion()"
            :style="next ? 'background-color: rgb(106, 128, 202)' : ''"
          >
            Skip
          </button>
          <button
            @click="nextQuestion()"
            :style="!next ? 'background-color: rgb(106, 128, 202)' : ''"
          >
            Next
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
export default {
  data() {
    return {
      questions: [
        {
          question: "Who was the first president of independent India",
          propositions: [
            { props: "Rajendra Prasad", correct: true },
            { props: "Sarvepalli Radhakrishnan" },
            { props: "Jawaharlal Nehru" },
            { props: "Lal Bahadur Shastri" },
          ],
        },
        {
          question: "Which country will host 2022 FIFA WORLD CUP?",
          propositions: [
            { props: "ARGENTINA" },
            { props: "BRASIL" },
            { props: "QATAR", correct: true },
            { props: "RUSSIA" },
          ],
        },
        {
          question: "WHO WROTE THE BOOK 'DA VINCI CODE' ?",
          propositions: [
            { props: "Jane Austen" },
            { props: "CHARLES DICKENS" },
            { props: "DAN BROWN", correct: true },
            { props: "VIRGINIA WOOLF" },
          ],
        },
        {
          question: "How to write an IF statement in JavaScript ?",
          propositions: [
            { props: "if i = 5 then" },
            { props: "if (i == 5)", correct: true },
            { props: "if i == 5 then" },
            { props: "if i = 5" },
          ],
        },
        {
          question: "WHICH OF THE FOLLOWING MOVIE WON AN OSCAR",
          propositions: [
            { props: "3 IDIOTS" },
            { props: "American Psycho" },
            { props: "Rebel Without a Cause" },
            { props: "LA LA LAND", correct: true },
          ],
        },
        {
          question: "Which Tennis player won the Mexican Open Title 2022",
          propositions: [
            { props: " Novak Djokovic" },
            { props: "Rafael Nadal", correct: true },
            { props: "Roger Federer" },
            { props: "Daniel Medvedev" },
          ],
        },
      ],
      a: 0,
      b: 1,
      next: true,
      score_show: false,
      quiz: true,
      score: 0,
      correct: false,
      progress: 0,
    };
  },
  name: "App",
  components: {
    //HelloWorld
  },
  computed: {},
  methods: {
    selectResponse(e) {
      this.correct = true;
      this.next = false;
      if (e.correct) {
        this.score++;
      }
    },
    check(status) {
      if (status.correct) {
        return "correct";
      } else {
        return "incorrect";
      }
    },
    nextQuestion() {
      if (this.next) {
        return;
      }
      this.progress = this.progress + 100 / this.questions.length;
      if (this.questions.length - 1 == this.a) {
        this.score_show = true;
        this.quiz = false;
      } else {
        this.a++;
        this.b++;
        this.correct = false;
        this.next = true;
      }
    },
    skipQuestion() {
      if (!this.next) {
        return;
      }
      this.progress = this.progress + 100 / this.questions.length;
      if (this.questions.length - 1 == this.a) {
        this.score_show = true;
        this.quiz = false;
      } else {
        this.a++;
        this.b++;
      }
    },

    restartQuiz() {
      Object.assign(this.$data, this.$options.data()); // reset data in vue
    },
  },
};
</script>
