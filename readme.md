# wm-lib
An ISAM Infomap Library

Version: 0.6

## Library Functions:

- generateJWT()
- base64URLEncode()
- performGET()
- performPOST()
- generateUUID()

### wm.generateJWT()
Function:  Returns a signed JWT  

Usage: wm.generateJWT(header, payload, secret)  
where {header} and {payload} are JSON objects or strings, and secret is a string

Example:

    var header = {};
    header.alg = "HS256";
    header.typ = "JWT";

    var body = {};
    body.user = "Alice";

    var secret = "Passw0rd";

    mySignedJWT = wm.generateJWT(header, body, secret);

### wm.base64URLEncode()
Function: Returns a base64URL encoded version of input string

Usage: wm.base64URLEncode(data)  
where {data} is a string

Example:

    var plaintext = "This string is readable";
    var base64URLSafe = wm.base64URLEncode(plaintext);

### wm.performGET()
Function: Performs an HTTP GET request, returns a results object

Response Object:    

	.code - the HTTP Status code
	.body - the HTTP response body
	.headers - a hash table of response headers

Usage: wm.performGET({url}, {headers}, [debug])

where {url} is the URL to get, {headers} is an ISAM headers object, [debug] is an optional boolean to increase logging

Example:

	var headers = new Headers();
	headers.addHeader("iv-user", "testuser");
	headers.addHeader("foo", "bar");

	resultObject = wm.performGET("https://example.com/",headers);

	responseCode = resultObject.code;
	responseBody = resultObject.body;
	responseHeaders = resultObject.headers;
	referrer = resultObject.headers["referrer"];

### wm.performPOST()
Function: Performs an HTTP POST request, returns a results object

Response Object:    

	.code - the HTTP Status code
	.body - the HTTP response body
	.headers - a hash table of response headers

Usage: wm.performPOST({url}, {headers}, {data}, [debug])

where {url} is the URL to get, {headers} is an ISAM headers object, {data} is the post data, [debug] is an optional boolean to increase logging

Example:

	var headers = new Headers();
	headers.addHeader("iv-user", "testuser");
	headers.addHeader("foo", "bar");

	var postData = '{"foo":"bar"}';
	resultObject = wm.performPOST("https://example.com/", headers, postData);

	responseCode = resultObject.code;
	responseBody = resultObject.body;
	responseHeaders = resultObject.headers;
	referrer = resultObject.headers["referrer"];

### wm.generateUUID()
Function: Returns a randomly generated UUID

Response: A UUID. E.g. 005f5c9b-1949-4a04-ab9d-0a542317a5d5

Usage: wm.generateUUID()

Example:

    //Create a unique ID to track this instance of this infomap running.
    
    var runid = wm.generateUUID();

    function log(message) {
      IDMappingExtUtils.traceString("[" + runid + "] " + message);
    }

    log("Infomap started");



## Installation

To install the library, upload lib-wm.js as a new mapping rule to ISAM (Secure Access Control -> Mapping Rules).

In the mapping rule where you want to use the library functions, include the library with

    importMappingRule("lib-wm");

## License

The library itself includes the CryptoJS library, which is free for reuse and modification as long as the copyright headers are unchanged.

The non-CryptoJS code is [MIT Licensed](https://en.wikipedia.org/wiki/MIT_License), so feel free to re-use and modify.
