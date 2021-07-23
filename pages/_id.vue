<template>
  <div>
    <v-row class="my-10">
      <v-col cols="4" xl="1" lg="2" md="2" sm="3">
        <v-btn width="100%" to="/"
          ><v-icon class="pr-5">mdi-keyboard-backspace</v-icon>Back</v-btn
        >
      </v-col>
    </v-row>
    <v-row class="d-flex justify-space-between">
      <v-col cols="12" xl="6" lg="6" class="pr-xl-16 pr-lg-16">
        <v-img :src="country.flag" height="500"></v-img>
      </v-col>
      <v-col cols="12" xl="6" lg="6" class="pt-16 pl-xl-16 p-lg-16">
        <h2 class="mb-5">{{ country.name }}</h2>
        <v-row
          ><v-col>
            <p>Native Name: {{ country.nativeName }}</p>
            <p>Population: {{ country.population }}</p>
            <p>Region: {{ country.region }}</p>
            <p>Sub Region: {{ country.subregion }}</p>
            <p>Capital: {{ country.capital }}</p></v-col
          >
          <v-col>
            <p v-for="level in country.topLevelDomain" :key="level">
              Top Level Domain: {{ level }}
            </p>
            <p v-for="currency in country.currencies" :key="currency.name">
              Currencies: {{ currency.name }}
            </p>
            <p v-for="language in country.languages" :key="language.name">
              Languages: {{ language.name }}
            </p>
          </v-col></v-row
        >
        <v-row class="d-flex justify-center mt-16">
          <v-col cols="12" xl="3" lg="3">Border Countries:</v-col>
          <v-col cols="12" xl="9" lg="9"> 
            <v-row class="d-flex justify"
              ><v-col
                cols="5"
                v-for="border in nameOfBorders"
                :key="border"
                ><v-btn class="px-2 overflow" width="100%" :to="`/${border}`" >{{ border }}</v-btn></v-col
              ></v-row
            >
          </v-col>
        </v-row>
      </v-col>
    </v-row>
  </div>
</template>
<script>
export default {
  data() {
    return {
      country: [],
      nameOfBorders: [],
    }
  },
  async created() {
    const res = await this.$axios.get(
      `https://restcountries.eu/rest/v2/name/${this.$route.params.id}`
    )
    console.log('res', res.data[0])
    this.country = res.data[0]
    const borders = res.data[0].borders
    console.log(borders)
    // const getALl = await this.$axios.get('https://restcountries.eu/rest/v2/all')
    // console.log('getALl', getALl.data)
    for (const border of borders) {
      console.log('border', border)
      const result = await this.$axios.get(
        `https://restcountries.eu/rest/v2/alpha/${border}`
      )
      console.log('-------', result)
      this.nameOfBorders.push(result.data.name)
      console.log('nameOfBorders', this.nameOfBorders)
    }
  },
}
</script>
<style lang="scss" scoped>
.overflow{
    overflow-x: hidden;
}
.v-icon{
    font-size: 16px;
}
</style>