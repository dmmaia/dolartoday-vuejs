<template>
<div class="converter-container">
  <div><h2>US$:</h2><input v-model="moedaA_value" type="number" /></div>
  <h2>R$: {{moedaB_value}}</h2>
  <button v-on:click="converter">Converter</button>
</div>
</template>

<script>
  export default {
    name: 'Converter',

    data(){
      return {
        moedaA_value: 1,
        moedaB_value: 0,
        cotacao: 0,
      };
    },

    methods: {
      requestCotacao(){
        let url = "https://free.currconv.com/api/v7/convert?q=USD_BRL&compact=ultra&apiKey=590a41dfbd78a12428b8";

        fetch(url).then(res => {return res.json()})
        .then(json=>{
          this.cotacao = json["USD_BRL"];
          this.converter();
        })
      },

      converter() {
          this.moedaB_value = (this.cotacao * parseFloat(this.moedaA_value))
          .toFixed(2)
          console.log(this.cotacao)
      }
    },

    created(){
      this.requestCotacao();
    }
  }
</script>

<style>
  .converter-container {
    display: flex;
    flex-direction: column;
    max-width: 200px;
    align-items: center;
    justify-content: center;
  }
  .converter-container div{
    flex-direction: row;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .converter-container div input {
    margin-left: 8px;
    font-size: 20px;
    max-width: 150px;
}
</style>