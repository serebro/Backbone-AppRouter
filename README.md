# Backbone AppRouter

Extends Backbone.Router to get back a route pattern and construct an URL with arguments.

## Methods

	var myrouter = Backbone.Router.extend({
				routes: {
					'home'                         : 'home',
					'catalogue'                    : 'catalogue',
					'catalogue/:tags'              : 'catalogue',
					'catalogue/:productId/:rewrite': 'productSheet',
					'search/*'                     : 'search'
				},
				home: function(){
					console.log('ROUTER -> home'); 
				},
				catalogue: function(tag){
					if(!_.isUndefined(tag))
					{
						console.log('ROUTER -> catalogue -> tags -> '+ tag);
					}
					else
					{
						console.log('ROUTER -> catalogue');
					}
				},
				productSheet: function(productId)
				{
					console.log('ROUTER -> catalogue -> productId -> '+ productId);
				},
				search: function(query)
				{
					console.log('ROUTER -> search -> query -> '+ query);
				}
			});

	app.router = new router(); 

### setRoute

Wrap __reverse__ and __createUri__ methods in a single call. If multiple possibilities, try to find the good route by comparing the numbers of arguments with giving hash 

	var catalogueRoute = myrouter.setRoute('catalogue', ['awsome-tag']);
	console.log("create URI: %s", catalogueRoute);

### reverse

return an array of matching routes based on method name

	var productRoute = myrouter.reverse('productSheet');
	console.log("get reverse route: %s", productRoute[0]);

### createUri

return an URL base on the route pattern and an array of arguments

	var newProductUrl = app.router.createUri(productRoute[0], [321, 'anoter-product-name'])
	console.log("create route: %s", newProductUrl);

### productRoute

return the ordonned list of arguments for a route pattern

	myrouter.getArgs(productRoute);