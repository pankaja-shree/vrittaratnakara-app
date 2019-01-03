<template>
  <v-layout
    wrap
    style="height: 200px;"
  >

        <v-btn
          color="secondary"
          dark 
          round
          @click.stop="drawer = !drawer"
          class="ma-4 font-weight-bold text-capitalize"
        >
          All Lessons
        </v-btn>

    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="mini"
      class="primary"
      absolute
      dark
      temporary
    >
      <v-list class="pa-1">
        <v-list-tile dark v-if="mini" @click.stop="mini = !mini">
          <v-list-tile-action>
            <v-icon>chevron_right</v-icon>
          </v-list-tile-action>
        </v-list-tile>

        <v-list-tile avatar tag="div">
          <v-list-tile-avatar>
            <v-icon>library_books</v-icon>
          </v-list-tile-avatar>

          <v-list-tile-content>
            <v-list-tile-title>Lessons</v-list-tile-title>
          </v-list-tile-content>

          <v-list-tile-action>
            <v-btn icon @click.stop="mini = !mini">
              <v-icon>chevron_left</v-icon>
            </v-btn>
          </v-list-tile-action>
        </v-list-tile>
      </v-list>

      <v-text-field
        v-model="searchlist"
        append-icon="search"
        label="Search"
        single-line
        class = "px-3"
      ></v-text-field>
      
      <v-list class="pt-0" dense>
        <v-divider light></v-divider>

      <div v-for="item in items" :key="item.title" active-class="yellow--text">

        <v-list-group active-class="yellow--text" v-if="item.group" value="true">

          <v-list-tile active-class="yellow--text" dark slot="activator" router :to="item.to">
            <v-list-tile-action>{{ item.sl_num }}.</v-list-tile-action>
            <v-list-tile-title>{{item.title}}</v-list-tile-title>
          </v-list-tile>

          <div v-for="subitem in item.subitems" :key="subitem.title">

          <v-list-group active-class="yellow--text" v-if="subitem.subgroup" sub-group>

            <v-list-tile active-class="yellow--text" slot="activator" class="link" router :to="subitem.to">
              <v-list-tile-action>{{subitem.sl_num}}</v-list-tile-action>
              <v-list-tile-title>{{subitem.title}}</v-list-tile-title>
            </v-list-tile>

            <div v-for="div in subitem.divs" :key="div.title">

              <v-list-group active-class="yellow--text" v-if="div.types" sub-group>

                <v-list-tile active-class="yellow--text" slot="activator" class="link" router :to="div.to">
                  <v-list-tile-action>{{div.sl_num}}</v-list-tile-action>
                  <v-list-tile-title>{{div.title}}</v-list-tile-title>
                </v-list-tile>

                <v-list-tile active-class="yellow--text" v-for="vritta in div.vrittas" :key="vritta.title" class="link" router :to="vritta.to">
              <v-list-tile-action>{{vritta.sl_num}}</v-list-tile-action>
              <v-list-tile-title>{{vritta.title}}</v-list-tile-title>
            </v-list-tile>

              </v-list-group>

            <v-list-tile active-class="yellow--text" v-else class="link" router :to="div.to">
              <v-list-tile-action>{{div.sl_num}}</v-list-tile-action>
              <v-list-tile-title>{{div.title}}</v-list-tile-title>
            </v-list-tile>

            </div>

          </v-list-group>

          <v-list-tile active-class="yellow--text" class="link" v-else router :to="subitem.to">
            <v-list-tile-action>{{subitem.sl_num}}</v-list-tile-action>
            <v-list-tile-title>{{subitem.title}}</v-list-tile-title>
          </v-list-tile>

          </div>

        </v-list-group>

        <v-list-tile active-class="yellow--text" class="link" v-else router :to="item.to">
           <v-list-tile-action>{{ item.sl_num }}. </v-list-tile-action>

          <v-list-tile-content>
            <v-list-tile-title>{{ item.title }}</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>

        </div>

         
      </v-list>
    </v-navigation-drawer>
  </v-layout>
</template>

<script>
  export default {
    data () {
      return {
        drawer: null,
        searchlist: '',
        titles: [
          {
            title: 'Introduction',
            sl_num: '1',
            group: false,
            to: '/lessons/1'
          },
          {
            title: 'Identifying a Guru',
            sl_num: '2',
            group: false,
            to: '/lessons/2'
          },
          {
            title: 'Identifying a Laghu',
            sl_num: '3',
            group: false,
            to: '/lessons/3'
          },
          {
            title: 'Classification of Chandas',
            sl_num: '4',
            group: true,
            to: '/lessons/4',
            subitems: [
              {
                title: 'Varna Chandas',
                sl_num: '4.1',
                subgroup: true,
                to: '/lessons/4.1',
                divs: [
                  {
                    title: 'Samam',
                    sl_num: 'i',
                    types: 'true',
                    to: '/lessons/4.1.i',
                    vrittas: [
                      {
                        title: 'Uktā',
                        sl_num: 'I',
                        to: '/lessons/4.1.i.I'
                      },
                      {
                        title: 'Atyuktā',
                        sl_num: 'II',
                        to: '/lessons/4.1.i.II'
                      },
                      {
                        title: 'Madhyā',
                        sl_num: 'III',
                        to: '/lessons/4.1.i.III'
                      },
                      {
                        title: 'Pratishta',
                        sl_num: 'IV',
                        to: '/lessons/4.1.i.IV'
                      },
                      {
                        title: 'Supratishta',
                        sl_num: 'V',
                        to: '/lessons/4.1.i.V'
                      },
                      {
                        title: 'Gayatri',
                        sl_num: 'VI',
                        to: '/lessons/4.1.i.VI'
                      },
                      {
                        title: 'Ushnik',
                        sl_num: 'VII',
                        to: '/lessons/4.1.i.VII'
                      },
                      {
                        title: 'Anushtup',
                        sl_num: 'VIII',
                        to: '/lessons/4.1.i.VIII'
                      },
                      {
                        title: 'Bruhati',
                        sl_num: 'IX',
                        to: '/lessons/4.1.i.IX'
                      },
                      {
                        title: 'Pankti',
                        sl_num: 'X',
                        to: '/lessons/4.1.i.X'
                      },
                      {
                        title: 'Trishtup',
                        sl_num: 'XI',
                        to: '/lessons/4.1.i.XI'
                      },
                      {
                        title: 'Jagati',
                        sl_num: 'XII',
                        to: '/lessons/4.1.i.XII'
                      },
                      {
                        title: 'Atijagati',
                        sl_num: 'XIII',
                        to: '/lessons/4.1.i.XIII'
                      },
                      {
                        title: 'Shakvari',
                        sl_num: 'XIV',
                        to: '/lessons/4.1.i.XIV'
                      },
                      {
                        title: 'Atishakvari',
                        sl_num: 'XV',
                        to: '/lessons/4.1.i.XV'
                      },
                      {
                        title: 'AshtiH',
                        sl_num: 'XVI',
                        to: '/lessons/4.1.i.XVI'
                      },
                      {
                        title: 'AtyashtiH',
                        sl_num: 'XVII',
                        to: '/lessons/4.1.i.XVII'
                      },
                      {
                        title: 'DhrutiH',
                        sl_num: 'XVIII',
                        to: '/lessons/4.1.i.XVIII'
                      },
                      {
                        title: 'AtidhrutiH',
                        sl_num: 'XIX',
                        to: '/lessons/4.1.i.XIX'
                      },
                      {
                        title: 'KrutiH',
                        sl_num: 'XX',
                        to: '/lessons/4.1.i.XX'
                      },
                      {
                        title: 'PrarutiH',
                        sl_num: 'XXI',
                        to: '/lessons/4.1.i.XXI'
                      },
                      {
                        title: 'AkrutiH',
                        sl_num: 'XXII',
                        to: '/lessons/4.1.i.XXII'
                      },
                      {
                        title: 'VikrutiH',
                        sl_num: 'XXIII',
                        to: '/lessons/4.1.i.XXIII'
                      },
                      {
                        title: 'SankrutiH',
                        sl_num: 'XXIV',
                        to: '/lessons/4.1.i.XXIV'
                      },
                      {
                        title: 'AtikrutiH',
                        sl_num: 'XXV',
                        to: '/lessons/4.1.i.XXV'
                      },
                      {
                        title: 'UtkrutiH',
                        sl_num: 'XXVI',
                        to: '/lessons/4.1.i.XXVI'
                      },
                      {
                        title: 'Dandakam',
                        sl_num: 'XXVII',
                        to: '/lessons/4.1.i.XXVII'
                      }
                    ]
                  },
                  {
                    title: 'Ardhasamam',
                    sl_num: 'ii',
                    types: 'true',
                    to: '/lessons/4.1.ii',
                    vrittas: [
                      {
                        title: 'upacitram',
                        sl_num: 'I',
                        to: '/lessons/4.1.ii.I'
                      },
                      {
                        title: 'drutamadhyā',
                        sl_num: 'II',
                        to: '/lessons/4.1.ii.II'
                      },
                      {
                        title: 'vegavatī',
                        sl_num: 'III',
                        to: '/lessons/4.1.ii.III'
                      },
                      {
                        title: 'bhadravirāṭ',
                        sl_num: 'IV',
                        to: '/lessons/4.1.ii.IV'
                      },
                      {
                        title: 'ketumatī',
                        sl_num: 'V',
                        to: '/lessons/4.1.ii.V'
                      },
                      {
                        title: 'ākhyānakī',
                        sl_num: 'VI',
                        to: '/lessons/4.1.ii.VI'
                      },
                      {
                        title: 'viparītākhyānakī',
                        sl_num: 'VII',
                        to: '/lessons/4.1.ii.VII'
                      },
                      {
                        title: 'hariṇaplutā',
                        sl_num: 'VIII',
                        to: '/lessons/4.1.ii.VIII'
                      },
                      {
                        title: 'aparavaktram',
                        sl_num: 'IX',
                        to: '/lessons/4.1.ii.IX'
                      },
                      {
                        title: 'puṣpitāgrā',
                        sl_num: 'X',
                        to: '/lessons/4.1.ii.X'
                      },
                      {
                        title: 'yavamatī',
                        sl_num: 'XI',
                        to: '/lessons/4.1.ii.XI'
                      },
                      {
                        title: 'viyoginī',
                        sl_num: 'XII',
                        to: '/lessons/4.1.ii.XII'
                      }
                    ]
                  },
                  {
                    title: 'Vishamam',
                    sl_num: 'iii',
                    types: 'true',
                    to: '/lessons/4.1.iii',
                    vrittas: [
                      {
                        title: 'padacaturūrdhvam',
                        sl_num: 'I',
                        to: '/lessons/4.1.iii.I'
                      },
                      {
                        title: 'āpīḍam',
                        sl_num: 'II',
                        to: '/lessons/4.1.iii.II'
                      },
                      {
                        title: 'kalikā',
                        sl_num: 'III',
                        to: '/lessons/4.1.iii.III'
                      },
                      {
                        title: 'lavalī',
                        sl_num: 'IV',
                        to: '/lessons/4.1.iii.IV'
                      },
                      {
                        title: 'amṛtadhārā',
                        sl_num: 'V',
                        to: '/lessons/4.1.iii.V'
                      },
                      {
                        title: 'udgatā',
                        sl_num: 'VI',
                        to: '/lessons/4.1.iii.VI'
                      },
                      {
                        title: 'saurabhakam',
                        sl_num: 'VII',
                        to: '/lessons/4.1.iii.VII'
                      },
                      {
                        title: 'lalitam',
                        sl_num: 'VIII',
                        to: '/lessons/4.1.iii.VIII'
                      },
                      {
                        title: 'upasthitapracupitam',
                        sl_num: 'IX',
                        to: '/lessons/4.1.iii.IX'
                      },
                      {
                        title: 'vardhamānam',
                        sl_num: 'X',
                        to: '/lessons/4.1.iii.X'
                      },
                      {
                        title: 'śuddhavirāḍārṣabham',
                        sl_num: 'XI',
                        to: '/lessons/4.1.iii.XI'
                      }
                    ]
                  },
                  {
                    title: 'Gatha',
                    sl_num: 'iv',
                    to: '/lessons/4.1.iv'
                  }
                ]
              },
              {
                title: 'Matra Chandas',
                sl_num: '4.2',
                subgroup: true,
                to: '/lessons/4.2',
                divs: [
                  {
                    title: 'Arya',
                    sl_num: 'i',
                    to: '/lessons/4.2.i',
                    types: true,
                    vrittas: [
                      {
                        title: 'Pathya',
                        sl_num: 'I',
                        to: '/lessons/4.2.i.I'
                      },
                      {
                        title: 'Vipula',
                        sl_num: 'II',
                        to: '/lessons/4.2.i.II'
                      },
                      {
                        title: 'Chapala',
                        sl_num: 'III',
                        to: '/lessons/4.2.i.III'
                      }
                    ]
                  },
                  {
                    title: 'Giti',
                    sl_num: 'ii',
                    to: '/lessons/4.2.ii',
                    types: true,
                    vrittas: [
                      {
                        title: 'Upagiti',
                        sl_num: 'I',
                        to: '/lessons/4.2.ii.I'
                      },
                      {
                        title: 'Udgiti',
                        sl_num: 'II',
                        to: '/lessons/4.2.ii.II'
                      },
                      {
                        title: 'Aryagiti',
                        sl_num: 'III',
                        to: '/lessons/4.2.ii.III'
                      }
                    ]
                  },
                  {
                    title: 'Vaitaliya',
                    sl_num: 'iii',
                    to: '/lessons/4.2.iii',
                    types: true,
                    vrittas: [
                      {
                        title: 'Aupacchandasikam',
                        sl_num: 'I',
                        to: '/lessons/4.2.iii.I'
                      },
                      {
                        title: 'Apatalika',
                        sl_num: 'II',
                        to: '/lessons/4.2.iii.II'
                      },
                      {
                        title: 'Dakshinantika',
                        sl_num: 'III',
                        to: '/lessons/4.2.iii.III'
                      },
                      {
                        title: 'Udicyavritti',
                        sl_num: 'IV',
                        to: '/lessons/4.2.iii.IV'
                      },
                      {
                        title: 'Prachyavritti',
                        sl_num: 'V',
                        to: '/lessons/4.2.iii.V'
                      },
                      {
                        title: 'Pravrittakam',
                        sl_num: 'VI',
                        to: '/lessons/4.2.iii.VI'
                      },
                      {
                        title: 'Aparantika',
                        sl_num: 'VII',
                        to: '/lessons/4.2.iii.VII'
                      },
                      {
                        title: 'Charuhasini',
                        sl_num: 'VIII',
                        to: '/lessons/4.2.iii.VIII'
                      }
                    ]
                  },
                  {
                    title: 'Vaktram',
                    sl_num: 'iv',
                    to: '/lessons/4.2.iv',
                    types: true,
                    vrittas: [
                      {
                        title: 'Pathyavaktram',
                        sl_num: 'I',
                        to: '/lessons/4.2.iv.I'
                      },
                      {
                        title: 'Viparītapathyāvaktram',
                        sl_num: 'II',
                        to: '/lessons/4.2.iv.II'
                      },
                      {
                        title: 'capalāvaktram',
                        sl_num: 'III',
                        to: '/lessons/4.2.iv.III'
                      },
                      {
                        title: 'yugmavipulā',
                        sl_num: 'IV',
                        to: '/lessons/4.2.iv.IV'
                      },
                      {
                        title: 'bhavipulā',
                        sl_num: 'V',
                        to: '/lessons/4.2.iv.V'
                      },
                      {
                        title: 'ravipulā',
                        sl_num: 'VI',
                        to: '/lessons/4.2.iv.VI'
                      },
                      {
                        title: 'navipulā',
                        sl_num: 'VII',
                        to: '/lessons/4.2.iv.VII'
                      },
                      {
                        title: 'tavipulā',
                        sl_num: 'VIII',
                        to: '/lessons/4.2.iv.VIII'
                      }
                    ]
                  },
                  {
                    title: 'mātrāsamavṛtta',
                    sl_num: 'v',
                    to: '/lessons/4.2.v',
                    types: true,
                    vrittas: [
                      {
                        title: 'acaladhṛtivṛttam',
                        sl_num: 'I',
                        to: '/lessons/4.2.v.I'
                      },
                      {
                        title: 'mātrāsamakam',
                        sl_num: 'II',
                        to: '/lessons/4.2.v.II'
                      },
                      {
                        title: 'viślokavṛttam',
                        sl_num: 'III',
                        to: '/lessons/4.2.v.III'
                      },
                      {
                        title: 'vānavāsikāvṛttam',
                        sl_num: 'IV',
                        to: '/lessons/4.2.v.IV'
                      },
                      {
                        title: 'citrāvṛttam',
                        sl_num: 'V',
                        to: '/lessons/4.2.v.V'
                      },
                      {
                        title: 'upacitrāvṛttam',
                        sl_num: 'VI',
                        to: '/lessons/4.2.v.VI'
                      },
                      {
                        title: 'pādākulakavṛttam',
                        sl_num: 'VII',
                        to: '/lessons/4.2.v.VII'
                      }
                    ]
                  },
                  {
                    title: 'śikhāvṛttam',
                    sl_num: 'vi',
                    to: '/lessons/4.2.vi'
                  },
                  {
                    title: 'khañjāvṛttam',
                    sl_num: 'vii',
                    to: '/lessons/4.2.vii'
                  },
                  {
                    title: 'anaṅgakrīḍāvṛttam',
                    sl_num: 'viii',
                    to: '/lessons/4.2.viii'
                  },
                  {
                    title: 'rucirāvṛttam',
                    sl_num: 'ix',
                    to: '/lessons/4.2.ix'
                  }
                ]
              }
            ]
          }
        ],
        mini: false,
        right: null
      }
    },
    computed: {
      items () {
        if (this.searchlist) {
          return this.titles.filter(item => {
            return item.title.includes(this.searchlist)
          })
        } else {
          return this.titles
        }
      }
    }
  }
</script>