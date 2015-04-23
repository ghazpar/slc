# SLC
Simple Lightweight Communications

## Example

```python
from slc import Socket

a, b, c, d = Socket(), Socket(), Socket(), Socket()
a.listen(31415) # listen() makes a server
b.listen(27182) # By default, listen on every interface
c.connect(31415, '127.0.0.1') # connect() makes a client
d.connect(31415, '127.0.0.1')
d.connect(27182, '127.0.0.1') # Multiple connects on a single socket are supported

# Send from client (c) to server (a)
c.send(b'Not all those who wander are lost.')
data = a.receive()

# Publish from server (a) to clients (c, d)
a.send(b'Time is a drug. Too much of it kills you.')
data1, data2 = c.receive(), d.receive()

# Publish from client (d) to servers (a, b)
d.send(b'The mirror does not reflect evil, but creates it.')
data1, data2 = a.receive(), b.receive()
```

## Features (work in progress)

* Simple, Lightweight and Portable
* Allows one-to-one and one-to-many (publisher - subscriber) communications
* Auto-reconnection on connection lost (TODO)
* Zero Configuration, service discovery (TODO)
* Throttling (TODO)
* Security (WIP)
* RPC (TODO)
* Support multiple backends (RDMA, UDP, IGMP, ...)
* Compression (WIP)

## API TODO

* Allow multiple listen from a single socket
* Allow socket to listen and connect at the same time
* Add source of message in receive()
* Add support for list of sources in receive()
* Add a way to know when the client is connected to the server. (method that returns if connection is successful for client or the number of clients successfully connected to the server)
* Support data more than 2**32 (maybe?)
