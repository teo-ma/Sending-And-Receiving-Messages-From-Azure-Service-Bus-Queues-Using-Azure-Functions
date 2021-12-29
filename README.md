# Sending-And-Receiving-Messages-From-Azure-Service-Bus-Queues-Using-Azure-Functions


Introduction

 

In this article, we are going to discuss about Service Bus Queue Trigger
in Azure Functions. We are also going to create a simple Azure function
to send and read messages from Service bus queues. So we are going to
create a HTTP trigger function to send messages to the queue and a
Service bus queue trigger function to read messages from the queue.

What is Azure Service Bus?

 

Azure Service Bus is a message broker service that is hosted on the
Azure platform and it provides functionality to publish messages to
various applications and also decouple the applications. Azure service
bus has two different flavors; i.e. Queues and Topics. Azure Service Bus
Queues follows a First-In-First-Out (FIFO) pattern. Queues provide
one-way transport like the sender is going to send messages in the queue
and the receiver would collect messages from the queue. In queues, there
is a 1:1 relationship between the sender and receiver. Messages are
present in the queue until the receiver processes and complete the
messages.
