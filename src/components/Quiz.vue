<template>
  <div>
      <h2>{{ quiz.titre }}</h2>
      <!--Ajout du nombre de question-->
      Nb Questions :
      {{ listeQuestions ? listeQuestions.length : 0 }}
      <button v-for="question in listeQuestions" :key="question.id">Question {{ question.id }}</button>
  </div>
</template>
<script>
import { getQuiz } from "../data/quiz";
import { getQuizAjax } from "../data/ajax";

export default {
  name: "Quiz",
  props: ["idQuiz"],
  data: function() {
    return {
      listeQuestions: null
    };
  },
  watch: {
    idQuiz: function() {
      if (this.idQuiz) {
        getQuizAjax(this.idQuiz).then(json => {
          this.listeQuestions = json;
        });
      }
    }
  },
  computed: {
    quiz : function() {
      return getQuiz(this.idQuiz);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
