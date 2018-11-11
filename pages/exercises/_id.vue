<template>
<v-container class="mt-0 pt-0">
  <v-layout row class="neg_margin">
  <v-btn color="accent darken-2" :ripple="{ class: 'error--text' }"  :to=previous><b>Previous</b></v-btn>
  <v-spacer></v-spacer>
  <v-btn color="accent darken-2" :ripple="{ class: 'error--text' }" :to=next><b>Next</b></v-btn>
  </v-layout>
<v-card color="accent lighten-4" class="mt-0 pt-0 bordered">
    <v-card-title primary-title>
        <h3 class="papyrus myheader">{{exercise.id}}. <span class="devanagari">{{exercise.title}}</span> <br>{{exercise.title_eng}}</h3>
         <v-chip :color="color" text-color="white" class ="title devanagari">
      <v-avatar class="green darken-4">{{score}}</v-avatar>
      Score
    </v-chip>
        </v-card-title>

      <v-layout row class="myheader3">
            <v-flex>
            <div class="devanagari px-1" v-html=exercise.question></div>
            </v-flex>
      </v-layout>
      <v-layout row class="myheader3">
            <v-flex>
                <v-radio-group column v-model="chosen" class="font-weight-bold">
                    <v-radio success="true" v-for="option, id in exercise.options" :key="id" :label="option" :value="option"></v-radio>
    </v-radio-group>
            <v-btn @click="check()" round color="error darken-2" :ripple="{ class: 'error--text' }" ><b>Submit</b></v-btn>
            <v-alert 
                v-model="success_alert"
                dismissible
                type="success"
                transition="scale-transition"
            >
            Correct Answer!
            </v-alert>
            <v-alert 
                v-model="fail_alert"
                dismissible
                type="error"
                transition="scale-transition"
            >
            Wrong Answer. Please try again or go through the relevant chapters.
            </v-alert>
            </v-flex>
          </v-layout>
  </v-card>
</v-container>
</template>

<script>
export default {
  data () {
    return {
      active: null,
      id: String(this.$route.params.id),
      exercise: '',
      index: '',
      prev_ex: '',
      next_ex: '',
      length: '',
      previous: '/',
      next: '/',
      chosen: null,
      success_alert: false,
      fail_alert: false,
      score: 0,
      color: 'red'
    }
  },
  layout: 'lessons',
  mounted () {
    // console.log(this.id)
    this.exercise = this.$store.state.exercises.find(ex => String(ex.id) === this.id)
  },
  created () {
    // console.log(this.$store.state.exercises.find(exercise => exercise.id === '4.1'))
    this.index = this.$store.state.exercises.findIndex(ex => String(ex.id) === this.id)
    this.prev_ex = this.$store.state.exercises[this.index - 1]
    this.next_ex = this.$store.state.exercises[this.index + 1]
    this.length = this.$store.state.exercises.length
    this.previous = this.index > 1 ? '/exercises/' + (this.prev_ex.id) : '/exercises/1'
    this.next = this.index < this.length - 1 ? '/exercises/' + (this.next_ex.id) : '/exercises/10'
    // console.log(this.index)
    // console.log(this.prev_exercise)
    // console.log(this.next_exercise.id)
    // console.log(this.$store.state.exercises)
    // console.log(this.$axios.$get('/exercises/' + this.$route.params.id))
  },
  methods: {
    nexttab () {
      const active = parseInt(this.active)
      this.active = (active < this.exercise.types - 1 ? active + 1 : 0)
    },
    check (ans) {
      let correct = this.exercise.ans
      if (this.chosen === correct) {
        let audio = new Audio('https://s3.ap-south-1.amazonaws.com/quiz-sounds/correct.wav')
        audio.play()
        this.success_alert = true
        this.fail_alert = false
        this.score = 1
        this.color = 'green'
      } else {
        let audio = new Audio('https://s3.ap-south-1.amazonaws.com/quiz-sounds/wrong.wav')
        audio.play()
        this.success_alert = false
        this.fail_alert = true
        this.score = 0
        this.color = 'red'
      }
    }
  }
}
</script>

<style scoped>
.bordered {
      border: 10px solid transparent;
-webkit-border-image: url('~/assets/img/border.png') 30 round; /* Safari 3.1-5 */
    -o-border-image: url('~/assets/img/border.png') 30 round; /* Opera 11-12.1 */
    border-image: url('~/assets/img/border.png') 30 round;
    border-radius: 15px;
    margin:0;
    padding: 2%;
}

 .neg_margin {
  margin-top: -10%;
}

</style>
