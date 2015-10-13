# very ez n simple currency converter 4 internets
This thingy uses [money.js](https://github.com/openexchangerates/money.js/) and [accounting.js](https://github.com/openexchangerates/accounting.js) with some funky jQuery to enable currency conversion on websites that dont support it (like bigcartel) take a look at [sharkweek.co.nz](http://sharkweek.co.nz) to see it in action.

#Installation
I use [open exchange rates](https://openexchangerates.org/) for the JSON data for currency, you'll need to get a app ID or use something else if you dont want to use openexchangerates.

On line 6 of the .js file, you can configure your rates URL

        var ezOpenRates = "https://openexchangerates.org/api/latest.json?app_id=[yourappid]";

Add the JS to your site @ the bottom.

        <script src="ez-currency-converter.js" type="text/javascript"></script>

##Get it goin'
Set up a document ready that creates the element.

        (function($){    
          $(document).ready(function(){
              $('.currency_converter').ezCurrency({
                  baseCurrency: 'NZD',
                  baseSign: '$',
                  currencies: ["AUD", "CAD", "GBP", "EUR", "JPY", "USD"],
                  curSign: ["$", "$", "£", "€", "¥", "$"]
              });
            });
        })(jQuery)


##Markup

###Currency Selector
Put the select box where you can change currencies somewhere on your site like this

        <select class="currency_converter"></select>
        
and the options will fill themselves.

###Prices 

        <span class="ezPrice">$69.00</span>
        
If you dont want a symbol to display, it would have the class no_symbol

        <span class="ezPrice no_symbol">$420.00</span>
