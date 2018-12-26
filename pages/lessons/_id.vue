<template>
<v-container class="mt-0 pt-0">
  <v-layout row class="neg_margin">
  <v-btn color="accent darken-2" :ripple="{ class: 'error--text' }"  :to=previous><b>Previous</b></v-btn>
  <v-spacer></v-spacer>
  <v-btn color="accent darken-2" :ripple="{ class: 'error--text' }" :to=next><b>Next</b></v-btn>
  </v-layout>
<v-card color="accent lighten-4" class="mt-0 pt-0 bordered">
    <v-card-title primary-title>
        <h3 class="papyrus myheader">{{lesson.id}}. <span class="devanagari">{{lesson.title_sans}}</span> <br>{{lesson.title_eng}}</h3>
        </v-card-title>

      <v-layout row class="myheader3">
            <v-flex xs6>
            <div class="devanagari px-1" v-html=lesson.definition_sans></div>
            </v-flex>
            <v-flex xs6>
            <div class="font-weight-bold px-1" v-html=lesson.definition_eng></div>
            </v-flex>
          </v-layout>
          <v-layout xs12 class="myheader3 devanagari px-1" v-html=lesson.common></v-layout>

          <div v-if='lesson.treeData'>
            <tree type="tree" class="tree" zoomable :data="treeData" node-text="name" layoutType="euclidean" :radius=4 @clicked="onClick"> 
            </tree>
          </div>

      <div v-if="lesson.types" class="myheader3">
        <div class="text-xs-center mt-3">
      <v-btn @click="nexttab">next tab</v-btn>
    </div>
    <v-tabs
      v-model="active"
      color="accent"
      dark
      slider-color="yellow"
    >
      <v-tab
        v-for="n in lesson.types"
        :key="n"
        ripple
        class="font-weight-bold"
      >
        {{ n }}

      </v-tab>
      <v-tab-item
        v-for="n in lesson.type"
        :key="n"
      >
        <v-card flat>
          <v-card-text class="devanagari" v-html="n.text_sans"></v-card-text>
        </v-card>
      </v-tab-item>
    </v-tabs>

  </div>
  </v-card>
  <v-layout row>
  <v-btn color="accent darken-2" :ripple="{ class: 'error--text' }"  :to=previous><b>Previous</b></v-btn>
  <v-spacer></v-spacer>
  <v-btn color="accent darken-2" :ripple="{ class: 'error--text' }" :to=next><b>Next</b></v-btn>
  </v-layout>
</v-container>
</template>

<script>
let tree
if (process.browser) {
  tree = require('vued3tree').tree
// use scrollmagic
}
export default {
  components: {
    tree
  },
  data () {
    return {
      active: null,
      id: String(this.$route.params.id),
      lesson: '',
      index: '',
      prev_lesson: '',
      next_lesson: '',
      length: '',
      previous: '/',
      next: '/',
      treeData: '',
      currentNode: null
    }
  },
  layout: 'lessons',
  mounted () {
    // console.log(this.id)
    this.lesson = this.$store.state.lessons.find(less => String(less.id) === this.id)
    this.treeData = this.lesson.treeData
    // console.log(this.treeData)
  },
  created () {
    // console.log(this.$store.state.lessons.find(lesson => lesson.id === '4.1'))
    this.index = this.$store.state.lessons.findIndex(lesson => String(lesson.id) === this.id)
    this.prev_lesson = this.$store.state.lessons[this.index - 1]
    this.next_lesson = this.$store.state.lessons[this.index + 1]
    this.length = this.$store.state.lessons.length
    this.previous = this.index > 1 ? '/lessons/' + (this.prev_lesson.id) : '/lessons/1'
    this.next = this.index < this.length - 1 ? '/lessons/' + (this.next_lesson.id) : '/lessons/4.2.ix'
    // console.log(this.index)
    // console.log(this.prev_lesson)
    // console.log(this.next_lesson.id)
    // console.log(this.$store.state.lessons)
    // console.log(this.$axios.$get('/lessons/' + this.$route.params.id))
  },
  methods: {
    nexttab () {
      const active = parseInt(this.active)
      this.active = (active < this.lesson.types - 1 ? active + 1 : 0)
    },
    onClick (evt) {
      window.open('/lessons/' + evt.data.url)
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

.tree {
  height: 2200px;
  width: 100%;
}
</style>
