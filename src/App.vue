<template>
  <div id="app">
    <label for="country_select">Select a Country:</label>
    <select id="country_select" v-model="selectedCountry">
      <option disabled value="">Select a country</option>
      <option v-for="country in countries" :key="country.alpha3code" :value="country">{{country.name}}</option>
    </select>

    <country-detail v-if="selectedCountry" :country="selectedCountry"></country-detail>

    <button v-on:click="addCountryToFaves">Add Country to favourites</button>

    <favourite-countries ></favourite-countries>
</div>

</template>

<script>
import CountryDetail from './components/CountryDetail.vue';
import FavouriteListItem from './components/FavouriteListItem.vue';

export default {
  name: 'App',
  data() {
    return {
      countries: [],
      selectedCountry: null,
      favouriteCountries: []
    }
  },
  components: {
    'country-detail': CountryDetail,
    'favourite-countries': FavouriteListItem
  },
    mounted(){
      this.fetchCountry()
    },
    methods: {
      fetchCountry: function(){
        fetch("https://restcountries.eu/rest/v2/all")
        .then(response => response.json())
        .then(country => this.countries = country)
      },
      addCountryToFaves: function(){
        self.favouriteCountries.push(selectedCountry)
      }
    }
}
</script>

<style>
.small-flag {
  height: 20px
}



</style>
