# Event Handler

Question
What is the earliest point at which the client can start sending data/messages to the server?

Correct Answer
As soon as the connection is successfully established. We need a way to be notified when that happens, though.

# JSON
What is JSON?
a way to convert objects into text
JSON is a subset of JavaScript that allows string-representation of objects

# Naming variables
You notice several variables are named ambiguously like data, info, and stuff. What specific advice from the style guide or clean code principles would you apply to give constructive feedback to your colleague?
he clean code principles emphasize the importance of meaningful names. You could suggest renaming data to something more descriptive like userData or customerInfo, depending on what the data represents. For info and stuff, recommend specific names that clearly describe what they contain, such as paymentDetails for info if it contains information about payments, and inventoryItems for stuff if it refers to items in an inventory.

How can we tell the HTTP response code (eg: 404) when using our browser?
The browser's DevTools offer this insight. In Chrome, we can check the Network tab which shows each request made and its resulting response code, among other details.

# EJS
What is the purpose of routing middleware in a web server?
- It defines application endpoints (URIs)
- Sends responses back to the client
- Matches requested routes using pattern expressions ('/ab*cd')

In Express, when an EJS template is rendered using res.render(), the EJS is evaluated on the server or client?
- On the server, before the HTTP response gets sent to the client

In a POST request, where are the parameters typically sent?
- Mainly in the request body, and sometimes the headers

How would you use cURL to make a POST request to http://example.com/api/endpoint
- curl -X POST http://example.com/api/endpoint

Note:
- the argumnet -d is used to send data
- the argument -b specifies a cookie
- the argument -LI this would follow redirections and show response headers

