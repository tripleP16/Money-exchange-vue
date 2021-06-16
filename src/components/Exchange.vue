<template>
    <div class="row indigo darken-4" id="contenido">
        <h4 class="white-text">Convertidor de Monedas</h4>
        <div class="col s5 white" id="us">
            <div class="row">
                <div class="col s2">
                    <img src="https://www.countryflags.io/us/flat/64.png">
                </div>
                <div class="col s6">
                    <h5>Estados Unidos</h5>
                </div>
            </div>
            <div class="row">
                <p>Valor de cambio {{usValue}} USD</p>    
                <div class="input-field col s6">
                    <input id="us_value" type="number" class="validate" v-model="dolars" @keyup="transformar">
                    <label class="active" for="us_value">Cantidad en dolares</label>
                </div>
            </div>
        </div> 
        <div class="col s2"></div> 
        <div class="col s5 white" id="other">
            <div class="row">
                <div class="col s2">
                    <img v-if='countryFlag' :src='countryFlag'>
                </div>
                <div class="col s6">
                    <h5>{{countryName}}</h5>
                </div>
            </div>
            <div class="row">
                <p>Valor de cambio {{exchange}} {{countrySymbol}}</p>    
                <div class="input-field col s7">
                    <input id="us_value" type="number" class="validate" v-model="value" @keyup="transformar">
                    <label class="active" for="us_value" >Cantidad en {{currency}}</label>
                </div>
            </div>
        </div>  
    </div>
</template>
<script>
    export default {
        name:"exchange-component", 
        props:{
            countryFlag:String, 
            exchange:Number, 
            countryName:String,
            countrySymbol:String,
            currency:String, 
            value:Number
        }, 
        data:function(){
            return {
                usValue:1,
                dolars:0,
            }
        }, 
        methods:{
            transformar:function(){
                this.dolars = this.value / this.exchange;
            }
        }

    }
</script>
<style>
    #contenido{
        padding: 2.5%;
    }
    #us{
        padding: 2.5%;
    }
    #other{
        padding: 2.5%;
    }
</style>