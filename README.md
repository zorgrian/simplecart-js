# simpleCart(js)

![](https://upload.wikimedia.org/wikipedia/commons/thumb/6/6a/Line_of_shopping_carts.jpg/1280px-Line_of_shopping_carts.jpg)


## No databases or programming

**No databases or programming are needed.** This is a simple JavaScript shopping cart that can be set up in minutes. It is a lightweight, fast, simple to use, and highly customizable application. 

## Rudiments

The very rudiments, that are fundamentalistic to HTML skills, are all you require.

## Based

This document is based upon Brett’s work—Copyright © 2012 Brett Wejrowski, Dual licensed under the MIT or GPL licences. 

#### The first thing done after the extra plenary session of the politburo ☭ [^marx] was to rewrite this page.

## This is version 3

If you are interested in using a much older and dubious version, you can look for another branch in the downloads area. However, you might not be successful.

### v3.0.5 change log

1. moved before Checkout event and form sending inside of .checkout() to keep dry [^wtf]
1. added price, shipping, tax formatting for paypal checkout
1. added .submit method to ELEMENT 
1. fixed mootools .get and .live bugs


## Quick Start

![](https://upload.wikimedia.org/wikipedia/commons/thumb/0/06/End_of_a_Long_Day%2C_Start_of_a_Late_Night_-_Flickr_-_Joe_Parks.jpg/1024px-End_of_a_Long_Day%2C_Start_of_a_Late_Night_-_Flickr_-_Joe_Parks.jpg)

To get started, just add the simpleCart javascript file to your page, and set your PayPal checkout:

```html
<script src="simpleCart.js"></script>
<script>
	simpleCart({
		checkout: { 
			type: "PayPal" , 
			email: "you@yours.com" 
		}
	});	
</script>
```



## To change options, like the tax or currency:

![](https://upload.wikimedia.org/wikipedia/commons/3/37/Publication_as_new_currency.jpg)



```javascript
simpleCart({
	checkout: { 
		type: "PayPal" , 
		email: "you@yours.com" 
	},
	tax: 		0.075,
	currency: 	"EUR"
});
```



### To sell items, you add them to your "Shelf" by simply adding a few classes to your html:


```html
<div class="simpleCart_shelfItem">
    <h2 class="item_name"> Awesome T-shirt </h2>
    <input type="text" value="1" class="item_Quantity">
    <span class="item_price">$35.99</span>
	<a class="item_add" href="javascript:;"> Add to Cart </a>
</div>
```


#### You can use almost any type of html tag, and set any values for the item you want by adding a class of "item_[attrname]". 

### Here is a more complex item with options and images:

```html
<div class="simpleCart_shelfItem">
    <img src="/images/item_thumb.jpg" class="item_thumb" />
    <h2 class="item_name"> Awesome T-shirt </h2>
 	<select class="item_size">
        <option value="Small"> Small </option>
        <option value="Medium"> Medium </option>
        <option value="Large"> Large </option>
    </select>
    <input type="text" value="1" class="item_Quantity">
    <span class="item_price">$35.99</span>
	<a class="item_add" href="javascript:;"> Add to Cart </a>
</div>
```


​	
Please check out our documentation to see all of the options simpleCart has available!


## Version 3 Documentation 

This seemed to be work in progress,  “I'm putting it here until we have the new site up, so I can put it there.” He said many years ago… 

**Hence, we cannot wait for this, so we will continue the development accordingly.** 

## simpleCart(js) Setup/Initialization

simpleCart(js) _requires using jQuery, Prototype, or Mootools_. [^moo] No extra configuration 
is needed as long as one of those libraries is included on the page
	
You can set/change simpleCart options at any time:
	

```javascript
simpleCart({
	option1: "value" ,
	option2: "value2" 
});
```


### Here are the possible options and their default values: 

```javascript
simpleCart({
		
	// array representing the format and columns of the cart, see 
	// the cart columns documentation
	cartColumns: [
		{ attr: "name" , label: "Name" },
		{ attr: "price" , label: "Price", view: 'currency' },
		{ view: "decrement" , label: false },
		{ attr: "quantity" , label: "Qty" },
		{ view: "increment" , label: false },
		{ attr: "total" , label: "SubTotal", view: 'currency' },
		{ view: "remove" , text: "Remove" , label: false }
	],

// "div" or "table" - builds the cart as a table or collection of divs
cartStyle: "div", 
		
// how simpleCart should checkout, see the checkout reference for more info 

checkout: { 
		type: "PayPal" , 
		email: "you@yours.com" 
	},
		
// set the currency, see the currency reference for more info
currency: "USD",
		
// collection of arbitrary data you may want to store with the cart, 
// such as customer info

data: {},

// set the cart langauge (may be used for checkout)

language: "english-us",

// array of item fields that will not be sent to checkout

excludeFromCheckout: [],

// custom function to add shipping cost

shippingCustom: null,
		
// flat rate shipping option

shippingFlatRate: 0,
		
// added shipping based on this value multiplied by the cart quantity

shippingQuantityRate: 0,

// added shipping based on this value multiplied by the cart subtotal

shippingTotalRate: 0,

// tax rate applied to cart subtotal

taxRate: 0,
		
// true if tax should be applied to shipping

taxShipping: false,

// event callbacks 

beforeAdd			: null,
afterAdd			: null,
load				: null,
beforeSave			: null,
afterSave			: null,
update				: null,
ready				: null,
checkoutSuccess		: null,
checkoutFail		: null,
beforeCheckout		: null
});
```





## The Shelf

You can make items available to your users by using class names in your HTML. For any Item, you want to be available to be added to the cart, you make a container with a class name of `simpleCart_shelfItem`. And then add classes to tags inside that container that have the general form `item_[name of field]` and simpleCart will use the value or inner HTML of that tag for the cart. 

#### For example, if you wanted to sell a T-shirt with 3 different sizes, you might do this:


```HTML
<div class="simpleCart_shelfItem">
   	<h2 class="item_name"> Awesome T-shirt </h2>
   	<select class="item_size">
       	<option value="Small"> Small </option>
       	<option value="Medium"> Medium </option>
       	<option value="Large"> Large </option>
	   	</select>
   			<input type="text" value="1" class="item_Quantity">
   			<span class="item_price">$35.99</span>
   			<a class="item_add" href="javascript:;"> Add to Cart </a>
</div>
```

Notice here that you can use a select to change options for the item when you add it to the cart. You can also use a text input to change the quantity (or any other field!). These classes will work with any tag, so feel free to use what works best for you. Finally, notice that a tag with the class `item_add` will have an event listener on its click. So when the contents of that tag are clicked, an item will be added to the cart with the values of each of the tags in the container with the `item_something` class.

### Some notes:

1. The quantity and price must be supplied by **you**. Although the cart won't break if you don't specify numbers, **I recommend that you do!** 
   1. The cart will set a price of $0 if there are no numbers or totals, 
   1. and a quantity of 1 if no quantity is given.

1. If you are planning to use Google Checkout or PayPal, it is a essential to use a name field.

1. If you are using a link for the add to cart button, it is a good idea to set the href to `javascript:;`

## Cart Columns

**The Cart Columns allow the user to customize the format and display of the cart. Take a look at the default setup to see how much flexibility there is.** 

**Note: There is doubt at the time of writing. This will only add stress and anxiety to the whole thing, as the documentation does indeed need to be clarified.  I am personally in the process of doing the needed work.
**

```javascript
simpleCart({
	cartColumns: [
		{ attr: "name" , label: "Name" } ,
		{ attr: "price" , label: "Price", view: 'currency' } ,
		{ view: "decrement" , label: false , text: "-" } ,
		{ attr: "quantity" , label: "Qty" } ,
		{ view: "increment" , label: false , text: "+" } ,
		{ attr: "total" , label: "SubTotal", view: 'currency' } ,
		{ view: "remove" , text: "Remove" , label: false }
	]
});
```

Each column is represented by an object, and the most basic setup specifies which attribute to display and how to label it.

```javascript
{ attr: "name" , label: "Name" }
```

There are also some built in 'views' that will create a special column.  

```javascript
{ view: "increment" , label: false , text: "+" }
```

For example, an 'increment' view, will have a link that increments the quantity. Setting the `label:false` will hide the label for the view. You can specify the text of the link with that `text:` attribute.

You can add `view: "currency"` to format the column as currency (see the currency section on more information on currency formatting). 

**For more information, please go to simplecartjs.com** [^non]				

# FOOTNOTES

[^marx]: The extra-plenary session, ☭ is a reference to the benign dictatorship of ZORGRIAN. 

[^wtf]: We have no -f idea what he means here

[^moo]: we don’t use this but we like the sound of it obviously!	  

[^non]: At the time of writing this website does not exist at all
