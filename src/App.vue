<template>
  <div id="app" class="container row">
    <div class="col-2">
				<select id='paises' class="browser-default" v-model="selected" @change="obtener">
					<option v-for="(country, index) in countriesFromApi" 
							:value="country" 
							:key='index' >{{country.name}} - {{country.currencyId}}</option>
				</select>
			</div>
      <br>
    <exchange-component :countryName="selected.name"
    :countryFlag="countryFlag"
    :countrySymbol="selected.alpha3"
    :currency="selected.currencyName"
    :exchange="exchangeValue"></exchange-component>
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
      selected:'', 
      countryFlag:'', 
      exchangeValue:0
      
    }
  },
  beforeCreate:function(){
	axios
	.get('https://free.currconv.com/api/v7/countries?q=USD_PHP&compact=ultra&apiKey=cd551d036c623e3af46d')
	.then((response) => {
	Object.entries(response.data.results).sort().forEach(([key, value])=>{
		console.log(key)
		this.countriesFromApi.push(value)
	})
	})
  }, 
  methods:{
    obtener:function(){
      console.log(this.selected.currencyId);
      this.countryFlag=`https://www.countryflags.io/${this.selected.id}/flat/64.png`
       axios.get(`https://free.currconv.com/api/v7/convert?q=USD_${this.selected.currencyId}&compact=ultra&apiKey=cd551d036c623e3af46d`)
            .then((response) => {
				Object.entries(response.data).sort().forEach(([key, value])=>{
               this.exchangeValue = value;
               console.log(key)
				})
		})
    }
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
