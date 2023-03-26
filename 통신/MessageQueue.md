https://aws.amazon.com/message-queue/


A message queue is a form of asynchronous service-to-service communication used in serverless and microservices architectures. Messages are stored on the queue until they are processed and deleted. Each message is processed only once, by a single consumer. 



https://aws.amazon.com/message-queue/features/


Push or Pull Delivery
Most message queues provide both push and pull options for retrieving messages. Pull means continuously querying the queue for new messages. Push means that a consumer is notified when a message is available (this is also called Pub/Sub messaging). You can also use long-polling to allow pulls to wait a specified amount of time for new messages to arrive before completing.


Schedule or Delay Delivery
Many message queues support setting a specific delivery time for a message. If you need to have a common delay for all messages, you can set up a delay queue.


At-Least-Once Delivery
Message queues may store multiple copies of messages for redundancy and high availability, and resend messages in the event of communication failures or errors to ensure they are delivered at least once.


Exactly-Once Delivery
When duplicates can't be tolerated, FIFO (first-in-first-out) message queues will make sure that each message is delivered exactly once (and only once) by filtering out duplicates automatically.


FIFO (First-In-First-Out) Queues
In these queues the oldest (or first) entry, sometimes called the “head” of the queue, is processed first. To learn more about Amazon SQS FIFO queues, refer to the Developer Guide.


Dead-letter Queues
A dead-letter queue is a queue to which other queues can send messages that can't be processed successfully. This makes it easy to set them aside for further inspection without blocking the queue processing or spending CPU cycles on a message that might never be consumed successfully.


Ordering
Most message queues provide best-effort ordering which ensures that messages are generally delivered in the same order as they're sent, and that a message is delivered at least once.


Poison-pill Messages
Poison pills are special messages that can be received, but not processed. They are a mechanism used in order to signal a consumer to end its work so it is no longer waiting for new inputs, and is similar to closing a socket in a client/server model.


Security
Message queues will authenticate applications that try to access the queue, and allow you to use encryption to encrypt messages over the network as well as in the queue itself. To learn more about queue security on AWS, read our blog, Server-Side Encryption for Amazon Simple Queue Service (SQS). You can also learn more about the security features of Amazon SQS in our Developer Guide.