<template>
<v-app class = "papyrus">
    <v-navigation-drawer
      :mini-variant.sync="miniVariant"
      :clipped="clipped"
      v-model="drawer"
      class="info"
      fixed
      app
    >
      <v-list>
        <v-list-tile
          router
          :to="item.to"
          :key="i"
          v-for="(item, i) in items"
          exact
        >
          <v-list-tile-action>
            <v-icon v-html="item.icon"></v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title v-text="item.title"></v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    <v-toolbar dark fixed app :clipped-left="clipped" color="primary">
      <v-toolbar-side-icon color="primary" @click="drawer = !drawer"></v-toolbar-side-icon>
      <v-toolbar-title v-text="title"></v-toolbar-title>
      <v-spacer></v-spacer>
        <v-btn flat icon to="/">
      <v-icon>home</v-icon>
        </v-btn>
      <span>Home</span>
    </v-toolbar>
    <v-content class = "bg3">
            <navleft />
        <nuxt />
    </v-content>
    <v-footer :fixed="fixed" color="primary" dark app>
      <span>&copy; 2018</span>
    </v-footer>
  </v-app>
</template>

<script>
import navleft from '~/components/lessonsnav.vue'
import navright from '~/components/rightnav.vue'

export default {
  data () {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        { icon: 'info', title: 'About us', to: '/aboutsf' },
        { icon: 'people', title: 'Credits', to: '/credits' },
        { icon: 'contact_support', title: 'Contact us', to: '/contact' }
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Interactive Tutorial on Vrittaratnakara'
    }
  },
  components: {
    navleft,
    navright
  }
}
</script>

<style scoped>
.bg3 {
  background: url("~/assets/img/bg3.jpg") no-repeat;
  background-size: cover;
}

.text-light {
  color: white;
}
</style>