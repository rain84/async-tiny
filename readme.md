# Async-tiny

##### A very tiny helper for working with Promise-workflow, which works around native "Promise"-object and which can help to work with async stuff and promises in more simple way. You should only receive "defer"-argument in your custom async functions , and invoke "resolve" or "reject" on it.

##### Your typical async-workflow will be looking like this

    asyncTiny
        .async( asyncFn1 )
        .async( asyncFn2 )
        .then( ... )
        .catch( ... )
        
        .....
        
        .asyncBundle( asyncTasks )
        .then( ... )
    ;

##### where "asyncFn1" and "asyncFn2" should looking like this

    function asyncFn(defer) {
        // ....some cool asynchronous code stuff....
        
        defer.resolve();
        // or   
        defer.reject();
    }

---------------------------------------------

##### Installation
    npm: npm i -D async-tiny
    github: git clone https://github.com/rain84/async-tiny.git


---------------------------------------------

##### **Methods :**
1. `async(fn)`
2. `asyncBundle([fn1, fn2, fn3, ...])`

---------------------------------------------

##### **Examples**
    
    //  Preparation functions for testing
    function asyncFn1( defer ) {
    	setTimeout( function () {
    		console.log( 'asyncFn-1' );
    		defer.resolve();
    	}, 1000 );
    }
    function asyncFn2( defer ) {
    	setTimeout( function () {
    		console.log( 'asyncFn-2' );
    		defer.resolve();
    	}, 500 );
    }
    function asyncTask1( defer ) {
    	setTimeout( function () {
    		console.log( 'asyncTask1' );
    		defer.resolve();
    	}, 1000 );
    }
    function asyncTask2( defer ) {
    	setTimeout( function () {
    		console.log( 'asyncTask2' );
    		defer.resolve();
    	}, 500 );
    }
    var tasks = [asyncTask1, asyncTask2,];
    
    
    //  Example of ".async()" usage
    function exampleAsync() {
    	console.log( 'Example of ".async()" starts' );
    
    	asyncTiny
    		.async( asyncFn1 )
    		.async( asyncFn2 )
    		.then( function () { console.log( 'Example of ".async()" done' ); } )
    	;
    }
    
    
    //  Example of ".asyncBundle()" usage
    function exampleAsyncBundle() {
    	console.log( 'Example of ".asyncBundle()" starts' );
    
    	asyncTiny.asyncBundle( tasks )
    		.then( function () { console.log( 'Example of ".asyncBundle()"  done' );} )
    	;
    }
    
    
    //  Complex example
    function exampleComplex() {
    	console.log( 'Complex example starts' );
    
    	asyncTiny
    		.async( asyncFn1 )
    		.catch( function ( err ) { console.log( 'asyncFn1 err. %s', err ); } )
    		.async( asyncFn2 )
    		.then( function () { console.log( 'async done' );} )
    
    		.asyncBundle( tasks )
    		.then( function () { console.log( 'Complex example done' ); } )
    	;
    }
    
    
    //exampleAsync();
    //exampleAsyncBundle();
    exampleComplex();
