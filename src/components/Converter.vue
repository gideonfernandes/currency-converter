<template>
  <div class="converter">
    <h2>{{currencyOne}} para {{currencyTwo}}</h2>
    <input type="text" v-model="currencyOne_value" v-bind:placeholder="currencyOne" />
    <button type="button" v-on:click="converter">Converter</button>
    <h3>{{currencyTwo_value}}</h3>
  </div>
</template>

<script>
  export default {
    name: 'Converter',
    props: ['currencyOne', 'currencyTwo'],
    data() {
      return {
        currencyOne_value: '',
        currencyTwo_value: 0
      }
    },
    methods: {
      converter() {
        let from_to = this.currencyOne + "_" + this.currencyTwo;        
        let api = 'https://free.currconv.com/api/v7/convert?q=' +
        from_to + '&compact=ultra&apiKey=1484ac5b346764020511';
 
        fetch(api)
          .then(response => {
            return response.json();
          })
          .then(data => {
            let priceQuote = data[from_to];
            this.currencyTwo_value = this.formatValue(
              (priceQuote * parseFloat(this.currencyOne_value)), this.currencyTwo
            );
        });
      },
      formatValue(value, currency) {
        if (currency == 'BRL') {
            return value.toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' });
        } else if (currency == 'USD') {
           return value.toLocaleString('en-US', { style: 'currency', currency: 'USD' });
        } else if (currency == 'EUR') {
          return value.toLocaleString('de-DE', { style: 'currency', currency: 'EUR' });
        } else if (currency == 'CAD') {
          return value.toLocaleString('en-CA', { style: 'currency', currency: 'CAD' });
        }
      }
    }
  }
</script>

<style scoped>
  .converter {
    max-width: 400px;
    padding: 20px;
    border-radius: 4px;
    background-color: #faf6f6;
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.4);
  }

  .converter > input {
    padding-left: 8px;
    height: 38px;
    border: 0;
    border-radius: 4px;
    min-width: 200px;
    color: #333;
  }

  .converter > button {
    cursor: pointer;
    height: 38px;
    border: 0;
    border-radius: 4px;
    margin-left: 12px;
    background-color: #2c3e50;
    color: #fff;
    transition: background-color 0.4s ease-in;
  }

  .converter > button:hover {
    background-color: #4b6681;
  }

  @media screen and (max-width: 768px) {
    .converter {
      width: 380px;
      margin: 8px auto;
    }
  }
</style>
