<div align="center">
<h1>NodeJS Currency Converter</h1>

<p>A minimal currency converter library for NodeJS that works out of the box.</p>
</div>

## Getting started

### Installation

This package can be installed using `npm`

```bash
npm install currency-converter-lt
```

or, `yarn`

```bash
yarn add currency-converter-lt
```

### Usage

Import `currency-converter-lt`.

```javascript
const CC = require('currency-converter-lt')
```

Then instantiate with either the empty constructor

```javascript
let currencyConverter = new CC()
```

Or, with a json object

```javascript
let currencyConverter = new CC({from:"USD", to:"JPY", amount:100})
```

The convert method will return the conversion based on the last conversion rate and can be used as a promise.

```javascript
currencyConverter.convert().then((response) => {
    console.log(response) //or do something else
})
```

`convert` can also take the amount as a parameter.

```javascript
currencyConverter.convert(100).then((response) => {
    console.log(response) //or do something else
})
```

To find the rates use the `rates` method.

```javascript
currencyConverter.rates().then((response) => {
    console.log(response) //or do something else
})
```

Rates can be cached for currency pairs. To implement rate caching, instantiate an object of CurrencyConverter only once in your project, in a CurrencyConverter file, and setup rates caching then import the instance of CurrencyConverter from the CurrencyConverter file in your project across the rest of your project. Use chaining to convert currencies when caching is implemented. Below is an example of a CurrencyConverter file.

Note: Rates are not actually deleted after the ratesCacheDuration. The rate remains in the rates cache of the CurrencyConverter object until a request is made for the same currency pair at which point, the old rate is overwritten.

```javascript
const CC = require('currency-converter-lt')

let currencyConverter = new CC()

let ratesCacheOptions = {
    isRatesCaching: true, // Set this boolean to true to implement rate caching
    ratesCacheDuration: 3600 // Set this to a positive number to set the number of seconds you want the rates to be cached. Defaults to 3600 seconds (1 hour)
}

currencyConverter = currencyConverter.setupRatesCache(ratesCacheOptions)

module.exports = currencyConverter
```

Chaining is also supported.

```javascript
currencyConverter.from("USD").to("GBP").amount(125).convert().then((response) => {
    console.log(response) //or do something else
})
```

## Disclaimer

This package uses web scraping to provide the api.

## License

This project is licensed under the [MIT](LICENSE) license.
