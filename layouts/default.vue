<template>
  <v-app>
    <v-app-bar fixed app>
      <v-container class="d-flex">
        <v-toolbar-title v-text="title" />
        <v-spacer />
        <v-btn text @click="makeDark()"
          ><v-icon
            class="px-2 pb-2"
            style="transform: rotate(40deg)"
            >mdi-moon-waxing-crescent</v-icon
          >Dark Mode</v-btn
        >
      </v-container>
    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      title: 'Where in the world?',
      darkMode: false,
    }
  },
  methods: {
    makeDark() {
      this.darkMode = !this.darkMode
      if(this.darkMode){
        this.$vuetify.theme.dark = true
      }
      else{
        this.$vuetify.theme.dark = false
      }
    },
  },
}
</script>
<style lang="scss" scoped>
body{
  font-family: 'NunitoSans-Regular';
}
</style>

