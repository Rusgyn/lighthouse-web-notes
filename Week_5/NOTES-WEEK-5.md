# Networking & HTTP for Web Developers

# Callback Review & Chaining
We use callbacks for :
  - modularity - we dont have to write the code over and over again.
  - reusability - we can reuse the functions.
  Callback chaining allows you to have nested functions that can feed results to each other.
  - Asynchronous - not returning values but instead use callback to passed the data.

# Error Handling
Try-catch blocks help us handle errors by letting us try something, and if it doesn’t work it will throw an error that will be caught.
error.name = Type Error
error..message = Assignment to constant variable.

Example:
```
let name = "John";
try {
  name = "Jane";
} catch (error) {
  console.log("There was an error ", error)
}
```

## Summary
we can use try-catch blocks to handle errors and use the error object in your code.

# Promise
A common use of Promises is when we want to run network requests to fetch data from APIs (e.g. information about the weather). We use .then, .catch, and .finally for when our Promise is fulfilled and for error handling.

## Conclusion
Promises help us both with handling errors and handling asynchronous functions. The Promises object in JavaScript can be either fulfilled, rejected, or pending. 

# Into to net

Net (net) is a module that is built into Node. It allows our Node apps to use TCP.

Example:

```
// Server.js

const net = require("net");//net allows our node apps to use TCP.
const server = net.createServer(); // start to implement or create a server.

let port = 3000;

server.on("connection", (client) => { // .on method listen for incoming connection.someone is now connected.
  
  console.log("New client connected"); // The server prints out New client connected!
  //OUTGOING
  client.write("Hello there!"); // .write method is writing data to the other party. Server send message to the client

  //INCOMING
  client.setEncoding("utf8"); // interpret data as text
  client.on("data", (data) => { // .on method - listen to the incoming data from other socket/party. The server prints out the data from the client. Receiving data from client.
    console.log("Message from client: ", data); //
  });

});

server.listen(port, () => { // .listen tells the server to turn "ON" and "listen".
  console.log(`Server is listening on port ${port}!`);
});

```

```
// CLient.js

const net = require("net"); //net allows our node apps to use TCP.

let port = 3000;

const conn = net.createConnection({ //creating a connection to our server using the port. client must follow the server port details to connect.
  host: "localhost",
  port: port, // same port with intend Server to connect to.
});

//INCOMING
conn.on("data", (data) => { // .on method - listen to the incoming data from other socket/party. The client prints out the data from the server. 
  console.log("Server says: ", data); // => Server says: Hello there!
});

//OUTGOING
conn.on("connect", () => { 
  conn.write("Hello from client!"); // client send a reply
});

conn.setEncoding("utf-8"); //interpret data as text

```

Output:
```
// Server
1. Server listening on port 3000!
2. New client connected!
3. Message from client: Hello from client!

// Client
1. Server says: Hello there!
```

## Conclusion

Client

- The client is always the one establishing the connection to the server. 
- All the client needs is the destination IP address and PORT information.

# Connect to the Server

## Events
When you connect to a server, or when it closes its connection with you, or when it sends you data, these are events. You can control how your client responds to these events if you know how to listen for them. If you don't listen for the event, you can't react to it.

## Event Handler
The conn object that Node gave you has everything you need to listen for events that occur on your connection. The code that defines what to do when an event occurs is often called an event handler.

The `.on` methods - lets you specify an event name and a function that does something when that event happens.

```
conn.on("event name", functionThatDoesSomething);
```

Syntax;
```
conn.on("event name", () => {
  // code that does something
});
```

The "event name" has to be a specific event name as defined by Node. For example, connect is a specific event that happens when a successful connection is made:

```
conn.on("connect", () => {
  // code that does something when the connection is first established
});
```

The "connect" event is triggered on a connection as soon as it is successfully established.

```
// Transmitting message to the sever from client. Sending a name.

  conn.on("connect", () => {
    conn.write("Name: RLM");
  });
```

Registering multiple callbacks for the same event is totally valid. They will be triggered in the sequence that they were registered.

Example:
```
// Connection Module. Script to establish a TCP connection and log incoming messages.

const net = require("net"); // net allows our node apps to use TCP.

let port = 50541;

// Establishes a connection to our intent game server
const connect = function() {
  
  const conn = net.createConnection({
    host: "localhost",
    port: port,
  });

  // Interpret incoming data as text
  conn.setEncoding("utf-8");

  // Handle incoming messages/data from the server. Event handler.
  conn.on("data", (data) => {
    console.log("Snake Host says: ", data);
  });

  // Connection event handler. Print message to the client screen when the connection is successfully established.
  conn.on("connect", () => {
    console.log("Successfully connected to game server");

    // Transmitting message to the sever. Sending a name.
    conn.write("Name: RLM");

    // Add multiple callbacks. Adding the supported move command by the game server.
    let time = 0;
    const movements = ["Move: up", "Move: left", "Move: up", "Move: right", "Move: right", "Move: down", "Move: down", "Move: right"];

    for (let movement of movements) {
      setTimeout(() => {
        conn.write(movement);
      }, time += 1000);
    }

  });

  return conn;
};

```


