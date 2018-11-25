<template>
  <v-layout column justify-center align-center class="papyrus">
    <v-flex xs12 sm8 md8>
      <div class="text-xs-center">
<sflogo title="संस्कृति-प्रतिष्ठानम्" subtitle1="Samskriti Foundation" subtitle2="presents" />
      </div>
      <v-card class = "bordered text-xs-center" color="primary" dark>
        <v-card-title class="myheader2 devanagari text-xs-center">वृत्तरत्नाकर-शिक्षकः - परस्परव्यवहारपूर्वकशिक्षणम्</v-card-title>
        <v-card-title class="myheader2 papyrus text-xs-center">Interactive tutorial for Vrittaratnakara</v-card-title>
        <v-card-text>
          <p>Interactive self learning software for learning Sanskrit prosody, various types of meters used in poetry.<v-btn color="accent" class="font-weight-bold text-capitalize" href="https://drive.google.com/file/d/1o1HzHNruyGN6TWmCkAjOaASHxdj-9IJB/view?usp=sharing" download>Download Word file of the website</v-btn></p>
          <p><v-btn color="accent" class="font-weight-bold text-capitalize" href="https://drive.google.com/file/d/1UgTWfUopAFDSFaQBC5ZHFb78080yPfcB/view?usp=sharing" download>Download PDF of the website</v-btn></p>
          <hr class="my-3">
        </v-card-text>
        <v-card-actions>
          <v-dialog v-model="dialog" scrollable>
          <v-btn slot="activator" round color="accent" class="text-capitalize font-weight-bold" large :ripple="{ class: 'error--text' }"> About <br> Vrittaratnakara</v-btn>
          <v-card color="info" class="papyrus bg1" light>
            <v-card-title class="myheader papyrus">Vrittaratnakara</v-card-title>
            <v-divider></v-divider>
            <v-card-text class="subheading papyrus font-weight-bold">Vritta Ratnakara of Kedara Bhatta (14th Century CE) is one of
the most popular texts on Sanskrit prosody. Though there are many books on Sanskrit prosody by eminent authors like Kalidasa, Kshemendra, etc, Vritta Ratankara continues to be an essential text for Sanskrit students. A speciality of this work is that the definition and illustration of a meter is given in one and the same verse. The verse defining a particular metre is composed in that particular meter itself. This is very helpful for a student of Sanskrit prosody. Another specialty of this work is that it is very brief – there are merely 136 verses. The author has covered all the prominent metres of Sanskrit literature in these verses.</v-card-text>
            <v-divider></v-divider>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="secondary" @click.native="dialog = false" ripple>Close</v-btn>
            </v-card-actions>
          </v-card>
          </v-dialog>
          <v-spacer></v-spacer>
          <v-btn round color="accent" class="font-weight-bold text-capitalize" nuxt to="/lessons" large>अध्यायाः<br>Learn</v-btn>
           <v-spacer></v-spacer>
          <v-btn round color="accent" class="font-weight-bold text-capitalize" nuxt to="/exercises" large>अभ्यासाः <br> Exercises</v-btn>
          <v-spacer></v-spacer>
          <v-btn round color="accent" class="font-weight-bold text-capitalize" nuxt to="/math" large>Mathematics in Sanskrit poetry</v-btn>
        </v-card-actions>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
import sflogo from '../components/SFLogo.vue'
export default {
  data: () => {
    return {
      dialog: false
    }
  },
  components: {
    sflogo
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

.bg1 {
  background:linear-gradient(0deg,rgba(241, 241, 171, 0.5),rgba(255, 255, 255, 0.2)),url(~/assets/img/bg3.jpg) no-repeat;
  background-size: cover;
  color: darkred;
}
</style>
