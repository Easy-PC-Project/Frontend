<template>
  <div>
        <Pregunta31/>
        <Pregunta32/>
        <Pregunta33/>
        <div class="">
          <vs-button @click="pushAnswer()"  to='/Summary' block class="boton-pop" color="rgb(59,22,100)">Aceptar</vs-button>
        </div>
  </div>
</template>

<script>
import Pregunta31 from "../Preguntas/Pregunta3.1.vue";
import Pregunta32 from "../Preguntas/Pregunta3.2.vue";
import Pregunta33 from "../Preguntas/Pregunta3.3.vue";

export default {
    name: "PopUpOpc3",
    components: {
        Pregunta31,
        Pregunta32,
        Pregunta33,
    },
    methods:{
      pushAnswer(){
        this.$store.commit("pushAnswers",this.$store.getters["getBudget"])
        this.$store.commit("pushAnswers",this.$store.getters["getCount"])
        this.$store.commit("pushAnswers",this.$store.getters["getA1"])
        this.$store.commit("pushAnswers",this.$store.getters["getA2"])
        this.$store.commit("pushAnswers",this.$store.getters["getA3"]) 
      },
      
    }
}
</script>

<style lang="scss" >
 .boton-pop {
  text-align: center;
  font-size: calc(1.2rem + 0.2vw);
  font-family: "Poppins", sans-serif;
}
</style>