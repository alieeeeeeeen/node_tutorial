# Node.js Tutorial

## REPL

A `REPL` means Read, Eval, Pring, Loop. It is a simple interactive computer programming envrionment that takes single user inputs, evaluates them, and returns the result to the user.

In a `REPL`, the user enters one or more expressions, and the REPL evaluates them and displays the results.

## Callback

A callback is an asynchronous equivalent for a function. A callback function is called at the completion of a given task. Node makes heavy use of callbacks.

`Blocking Code Example`
```javascript
var fs = require('fs');
var data = fs.readFileSync('filename.txt');
console.log(data.toString());
console.log('The program ended');
```

`Non-Blocking Code Example`
```javascript
var fs = require('fs');
fs.readFile('filename.txt', (err, data) => {
    if(err) console.error(err);
    console.log(data.toString());
})
console.log('The program ended');
```

The Blocking Code executed in sequence, whereas Non-blocking Code do not executed in sequence.

## Single-Thread

Node.js is a Single-Thread application, but it can support concurrency via the concept of **event** and **callback**. Node uses observer pattern.Node thread keeps an **event loop** and whenever a task gets completed, it fires the corresponding event which singals the event-listener function to execute.

### Event-Driven Programming

Node.js uses event heavily and it is also one of the reasons why Node.js is pretty fast compared to other similar language.
In a **event-driven** application, there is usually a main loop that listens for events, and then triggers a callback function when one of these events is dected. This pattern called **Observer**, like `mobx` and `rxjs`, which also have **Observer** pattern.

```javascript
var events = require('events');
// create eventEmitter object
var eventEmitter = new events.EventEmitter();

var connectionHandler = () => {
    console.log('connection successful');
    eventEmitter.emit('data_received');
}

eventEmitter.on('connection', connectionHanlder);
eventEmitter.on('data_received', () => {
    console.log('data received successfully');
})

console.log('Program ended');
```
### Async function

In Node.js, any async function accepts a callback function as the last parameter and the callback function accepts an error as the first parameter.

```javascript
var fs = require('fs');

fs.readFile('filename.txt', (err, data) => {
    if(err) console.error(err);
    console..log(data.toString());
})
```

## Stream

- Readable - Stream which is used for read operation
- Writable - Stream which is used for write operation
- Duplex - Stream which is used for both read and write operation
- Transform - A type of duplex stream where the output is computed based on the input.


### Readable Stream
```javascript
const fs = require('fs');
let data = '';

const readerStream = fs.createReadStream('input.txt');
readerStream.setEncoding('UTF8');

// to note that eventEmitter and event callback is the core of Node.js

readerStream.on('data', (chunk) => {
    data += chunk; // read the data from the file
});

readerStream.on('end', () => {
    console.log(data);
});

readerStream.on('error', (error) => {
    console.log(error.stack);
});
```

### Writable Stream

```javascript

const fs = require('fs');
const writableStream = fs.createWriteStream('output.txt');
const data = 'test';

writableStream.write(data, 'UTF8');

writableStream.on('end', () => {
    console.log(data);
})

writableStream.on('error', (error) => {
    console.log(error.stack);
})
```



# Reference
[Tutorialspoints](https://www.tutorialspoint.com/nodejs/nodejs_event_emitter.htm)
