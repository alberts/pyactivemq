# Sending pickled Python objects #

This example shows how to send pickled Python objects (in this case, [NumPy](http://www.scipy.org/) arrays).

http://code.google.com/p/pyactivemq/source/browse/trunk/src/examples/numpypickle.py

Expected output:

```
pickled 1000 arrays, each 80000 bytes, in 4.179399 seconds (18.2548 MiB/s)
```

# Asynchronous message listener #

The latest code in trunk supports asynchronous message listeners.

http://code.google.com/p/pyactivemq/source/browse/trunk/src/examples/asynclistener.py

Expected output (varies due to the threads associated with consumers):

```
consumer0 got: hello0
consumer1 got: hello0
consumer2 got: hello0
consumer0 got: hello1
consumer2 got: hello1
consumer1 got: hello1
...
consumer0 got: hello97
consumer0 got: hello98
consumer0 got: hello99
```

# Durable subscription #

This example corresponds to the DurableSubscriberExample.java described in the [Java EE 5 Tutorial](http://java.sun.com/javaee/5/docs/tutorial/doc/) in Chapter 31 under Creating Robust JMS Applications.

http://code.google.com/p/pyactivemq/source/browse/trunk/src/examples/DurableSubscriberExample.py

Expected output:

```
Starting subscriber
PUBLISHER: Publishing message: Here is a message 1
PUBLISHER: Publishing message: Here is a message 2
PUBLISHER: Publishing message: Here is a message 3
SUBSCRIBER: Reading Message: Here is a message 1
SUBSCRIBER: Reading Message: Here is a message 2
SUBSCRIBER: Reading Message: Here is a message 3
Closing subscriber
PUBLISHER: Publishing message: Here is a message 4
PUBLISHER: Publishing message: Here is a message 5
PUBLISHER: Publishing message: Here is a message 6
Starting subscriber
SUBSCRIBER: Reading Message: Here is a message 4
SUBSCRIBER: Reading Message: Here is a message 5
SUBSCRIBER: Reading Message: Here is a message 6
Closing subscriber
```