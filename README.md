# ez-js-json-currency-converter
This thingy uses [money.js](https://github.com/openexchangerates/money.js/) and [accounting.js](https://github.com/openexchangerates/accounting.js) with some funky jQuery to enable currency conversion on websites that dont support it (like bigcartel) take a look at [sharkweek.co.nz](http://sharkweek.co.nz) to see it in action.

#Installation
Add the JS to your site @ the bottom.

Set up a document ready that creates the element.



        (function($){    
          $(document).ready(function(){
              $('.currency_converter').ezCurrency({
                  baseCurrency: 'NZD',
                  currencies: ["AUD", "CAD", "GBP", "EUR", "JPY", "USD"],
                  curSign: ["$", "$", "£", "€", "¥", "$"]
              });
            });
        })(jQuery)

