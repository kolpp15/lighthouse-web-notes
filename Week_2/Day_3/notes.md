# W2D3 Notes

## Setting up Server to connect and send messages back and forth
```javascript
const net = require('net');
const port = 8018;

const server = net.createServer();

// this is to specify clients 
const connectClients = [];

const broadcast = (message) => {
    for (let connectedClient of connectClients){
        connectedClient.write(`someone said: ${message}`);
    }
};


server.listen(port, function() {
    // any lines written here will notify. This will happen whenever the client is 
    console.log(`Server is listening on port ${port}`);
});


// none of these (.on and .listen) schedule won't complete until it is done. So the order doesn't matter. the world 'connection' is important since it's listening for the 'connection'
server.on('connection', () => { // whatever types in the call back executes
    console.log(`client is connected`)
    
    // add the current client to the list of connected clients.
    connectClients.push(client);

    client.write('welcome to my awesome server!');

    // we need to setup a 'listen' to receive messages from the client. the word 'data' is important since the code is listening for 'data'.:
    client.on('data', (message) => {
        console.log(`Message received from client: ${message}`);
        broadcast(message);
    });
});
```

## Client's side 

```javascript
const net = require('net');
const port = 8018; 

//establish an object : name of the computer and the port
//need these two to show up on the server's side
const connectionInfo = {
    host: 'localhost',
    port: port
};

const cleint = net.createConnection(connectionInfo);

// we can have 2 event handler. See below:
client.on('connect', () => {
    console.log(`client is connected to the server.`)
});

client.on('data', (message) => {
    console.log(`server sent: ${message}`);
});

// to send back a message to server. we need a callback. whenever a client writes a message, it'll stdin. This is listening to the client's terminal (different from client.on above) :
process.stdin.on('data', (message) => {
    client.write(message);
});
```

