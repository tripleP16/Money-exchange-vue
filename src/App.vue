<template>
  <div id="app" class="container row">
    <div class="col-2">
				<select id='paises' class="browser-default" v-model="selected">
					<option v-for="(country, index) in countriesFromApi" 
							:value="country" 
							:key='index' >{{country.name}} - {{country.currencyId}}</option>
				</select>
			</div>
      <br>
    <exchange-component :countryName="selected.name"
    :countryFlag="selected.id"
    :countrySymbol="selected.alpha3"
    :currency="selected.currencyName"
    :exchange="1"></exchange-component>
  </div>
</template>

<script>
import '../node_modules/materialize-css/dist/css/materialize.css';
import '../node_modules/materialize-css/dist/js/materialize.js';
import ExchangeComponent from './components/Exchange.vue'; 
import axios from 'axios';
export default {
  name: 'App',
  components: {
    ExchangeComponent,
  },
  data:function(){
    return {
      countriesFromApi:[],
      selected:''
      
    }
  },
  beforeCreate:function(){
	axios
	.get('https://free.currconv.com/api/v7/countries?q=USD_PHP&compact=ultra&apiKey=cd551d036c623e3af46d')
	.then((response) => {
	Object.entries(response.data.results).sort().forEach(([key, value])=>{
		console.log(key)
    console.log(value)
		this.countriesFromApi.push(value)
	})
	})
  }, 
  beforeUpdate:function(){
    console.log(this.selected)
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
