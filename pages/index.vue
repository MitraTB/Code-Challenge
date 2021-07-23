<template>
  <div>
    <v-row class="d-flex justify-space-between mt-10">
      <v-col cols="12" xl="3" lg="3" md="6">
        <v-text-field
          label="Search"
          prepend-inner-icon="mdi-magnify"
          solo
          v-model="search"
        ></v-text-field>
      </v-col>
      <v-col cols="12" xl="3" lg="3" md="6">
        <v-select :items="items" label="Filter by Region" solo @change="filterByRegion(region)" v-model="region"></v-select>
      </v-col>
    </v-row>
    <v-row class="d-flex justify-space-between">
      <v-col
        cols="12"
        xl="3"
        lg="3"
        md="4"
        sm="6"
        v-for="country in searchCountry"
        :key="country.alpha2Code"
      >
        <nuxt-link :to="`/${country.name}`">
          <v-card>
            <v-img height="250" :src="country.flag"></v-img>
            <v-card-title>{{ country.name }}</v-card-title>
            <v-card-text>
              <p>Population: {{ country.population }}</p>
              <p>Region: {{ country.region }}</p>
              <p>Capital: {{ country.capital }}</p>
            </v-card-text>
          </v-card>
        </nuxt-link>
      </v-col>
    </v-row>
  </div>
</template>
<script>
export default {
  data() {
    return {
      items: ['Africa', 'Americas', 'Asia', 'Europe', 'Oceania'],
      countries: [],
      search: '',
      region:''
    }
  },
  async created() {
    const result = await this.$axios.get('https://restcountries.eu/rest/v2/all')
    this.countries = result.data
    console.log('countries', this.countries)
  },
  computed: {
    searchCountry() {
       return this.countries.filter(el=>{
        return el.name.toLowerCase().includes(this.search.toLowerCase())
      })
    },
  },
  methods:{
    async filterByRegion(reg){
      const res = await this.$axios.get(`https://restcountries.eu/rest/v2/region/${reg.toLowerCase()}`) 
      this.countries = res.data
      console.log('res',res)
    }
  }
}
</script>
<style lang="scss" scoped>
.v-icon{
  font-size: 14px;
}
</style>