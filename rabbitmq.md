# Setting up
After you `apt-get` it or obtain it by other means, one way to test it out is using `celery` on python. These notes are mostly `celery` specific, but the wider concepts apply to any MQ system.

1. Install `celery` if you haven't. Ideally do this in a python `virtualenv` to avoid polluting your global python installation with the zillion dependencies it needs.
1. Run `celery amqp`
1. Use the interactive shell to [kick the tires]( http://docs.celeryproject.org/en/latest/userguide/routing.html#hands-on-with-the-api)

(stolen and mildly paraphrased from the excellent celery documentation)

### What are exchanges, queues and routing keys?

1. Messages are sent to exchanges.
1. An exchange routes messages to one or more queues. Several exchange types exists, providing different ways to do routing, or implementing different messaging scenarios.
1. The message waits in the queue until someone consumes it.
1. The message is deleted from the queue when it has been acknowledged.

The steps required to send and receive messages are:

1. Create an exchange
1. Create a queue
1. Bind the queue to the exchange.

### What's the point of a routing key?
Exchanges can be created in many ways:
1. Direct Exchanges
2. Topic Exchanges
3. Any other exchanges available to RabbitMQ as plugins

Direct exchanges match on exact routing keys. A queue bound to a routing key only receives messages that contain the routing key.

Topic exchanges match by wildcard e.g. `testkey.*`  or  `*.testkey` or `#` (catch-all - matches everything) and route accordingly.

#### What if you do away with routing keys and have different queues instead?
For direct exchanges, the routing key decides which queue the message ends up in. If we use multiple queues they will still need routing keys, all messages without routing keys are promptly discarded by a direct exchange (Doesn't matter for fan-out exchanges which broadcast messages everywhere).
# TODO
Workflows involving multiple chained tasks:
[Canvas workflows](http://docs.celeryproject.org/en/latest/userguide/canvas.html)
