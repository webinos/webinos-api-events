# webinos events API #

**Service Type**: http://webinos.org/api/events

The main concept of events API is to !TODO!
The Webinos Event Handling API provides means to exchange data in terms of events among addressable entities (e.g., applications, services), either locally or remotely.

## Installation ##

To install the events API you will need to npm the node module inside the webinos pzp.

For end users, you can simply open a command prompt in the root of your webinos-pzp and do: 

	npm install https://github.com/webinos/webinos-api-events.git

For developers that want to tweak the API, you should fork this repository and clone your fork inside the node_module of your pzp.

	cd node_modules
	git clone https://github.com/<your GitHub account>/webinos-api-events.git
	cd webinos-api-events
	npm install


## Getting a reference to the service ##

To discover the service you will have to search for the "http://webinos.org/api/events" type. Example:

	var serviceType = "http://webinos.org/api/events";
	webinos.discovery.findServices( new ServiceType(serviceType), 
		{ 
			onFound: serviceFoundFn, 
			onError: handleErrorFn
		}
	);
	function serviceFoundFn(service){
		// Do something with the service
	};
	function handleErrorFn(error){
		// Notify user
		console.log(error.message);
	}

Alternatively you can use the webinos dashboard to allow the user choose the events API to use. Example:
 	
	webinos.dashboard.open({
         module:'explorer',
	     data:{
         	service:[
            	'http://webinos.org/api/events'
         	],
            select:"services"
         }
     }).onAction(function successFn(data){
		  if (data.result.length > 0){
			// User selected some services
		  }
	 });

## Methods ##

Once you have a reference to an instance of a service you can use the following methods:

###createWebinosEvent(type, addressing, payload, inResponseTo, withTimeStamp, expiryTimeStamp, addressingSensitive)

Creates a webinos Event.
         @param type Event type identifier.
         @param addressing References to the sending entity on the behalf of which the application wants to create the          event and to the event recipients.
         @param payload Event type-specific data or null (undefined is considered as equivalent to null).
         @param inResponseTo Event that this event is a response to (undefined is considered as equivalent to null).
         @param withTimeStamp Whether to set the generation timestamp (undefined is considered as equivalent to false).
         @param expiryTimeStamp Moment in time past which the event is no more valid or meaningful (undefined is      
         considered as equivalent to null).
         @param addressingSensitive Whether the addressing information is part of the informative content of the event 
         (undefined is considered as equivalent to false).

###addWebinosEventListener(listener, type, source, destination)

Registers an event listener.
         @param listener The event listener.
         @param type Specific event type or null for any type (undefined is considered as null).
         @param source Specific event source or null for any source (undefined is considered as null).
         @param destination Specific event recipient (whether primary or not) or null for any destination (undefined is          considered as null).
         @returns Listener identifier.

###removeWebinosEventListener(listenerId)

Unregisters an event listener.
         @param listenerId Listener identifier as returned by addWebinosEventListener().

###dispatchWebinosEvent(callbacks, referenceTimeout, sync)

Sends an event.
         @param callbacks Set of callbacks to monitor sending status (null and undefined are considered as equivalent 
         to a WebinosEventCallbacks object with all attributes set to null).
         @param referenceTimeout Moment in time until which the Webinos runtime SHALL ensure that the WebinosEvent 
         object being sent is not garbage collected for the purpose of receiving events in response to the event being 
         sent (null, undefined and values up to the current date/time mean that no special action is taken by the    
         runtime in this regard).
         @param sync If false or undefined, the function is non-blocking, otherwise if true it will block.


## Links ##

- [Specifications](http://dev.webinos.org/specifications/api/events.html)
- [Examples](https://github.com/webinos/webinos-api-events/wiki/Examples)

