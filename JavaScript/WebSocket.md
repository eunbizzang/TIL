https://javascript.info/websocket


To open a websocket connection, we need to create new WebSocket using the special protocol ws in the url:

```
let socket = new WebSocket("ws://javascript.info");
```
There’s also encrypted wss:// protocol. It’s like HTTPS for websockets.

Once the socket is created, we should listen to events on it. There are totally 4 events:
open – connection established,
message – data received,
error – websocket error,
close – connection closed.

example:
```
let socket = new WebSocket("wss://javascript.info/article/websocket/demo/hello");

socket.onopen = function(e) {
  alert("[open] Connection established");
  alert("Sending to server");
  socket.send("My name is John");
};

socket.onmessage = function(event) {
  alert(`[message] Data received from server: ${event.data}`);
};

socket.onclose = function(event) {
  if (event.wasClean) {
    alert(`[close] Connection closed cleanly, code=${event.code} reason=${event.reason}`);
  } else {
    // e.g. server process killed or network down
    // event.code is usually 1006 in this case
    alert('[close] Connection died');
  }
};

socket.onerror = function(error) {
  alert(`[error]`);
};
```
