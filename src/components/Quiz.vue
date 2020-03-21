<template>
  <div id="listequestions">
      <h2>{{ quiz.titre }}</h2>
      <!--Ajout du nombre de question-->
      Nb Questions :
      {{ listeQuestions ? listeQuestions.length : 0 }}
      <button @click="titrequestion" v-for="question in listeQuestions" :key="question.id">Question {{ question.id }}</button>
  </div>
</template>
<script>
import { getQuiz } from "../data/quiz";
import { getQuizAjax } from "../data/ajax";

var lesquestions = new Vue({
  el: '#listequestions',
  data: {
    name: 'Vue.js'
  },
  // Définissez les méthodes de l'objet
  methods: {
    titrequestions: function (event) {
      // `this` fait référence à l'instance de Vue à l'intérieur de `methods`
      document.write(<h3>{{ question.titre }}</h3>)
      // `event` est l'évènement natif du DOM
      if (event) {
        alert(event.target.tagName)
      }
    }
  }
})

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
