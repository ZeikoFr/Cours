# IoT

## Zone of interest

- Wireless channels can broadcast all messages to neighbors
    - Neighbors process messages if they wish

## Publish/Subscribe Paradigm

- Devices publish information tagged with categorie
    They broadcast to everyone

- Devices subscribe to some categories
    They act only on what they are interest in

- No tight coupling between publishers and subscribers
    Unmanaged loose coupling

## Publish/Subscribe Topologies

- With intermediary
    Publishers post messages to an intermediary  message broker
    Subscribers register subscriptions with that broker
    Broker perform filterinf and "store and forward" routing from publishers to subscribers
    The broker may prioritize messages in a queue before routing

- With intermediary 
    Each publisher and subscriber shares meta-data about each other via multicast
    Publishers and subscribers cache this information locally and route messages based on the discovery of each other interests

## Functional levels


## Web Naming

## What is MQTT

- ISO standard publish-subscribe-based lightweight messaging protocol
- Telemetry = tele-metering = remote measurements
- However, no message queuing in MQTT
- Lightweight = low network bandwidth and small code footprint
- For use on top of the TCP/IP protocol stack
- The publish-subscribe messaging pattern requires a message broker
- The broker is responsible for distributing messages to interested clients based on the topic of a message
- Data agnostic, adapt to any content formats

## Control messages

- Indicate the desired action to be performed on the identified resource/server
- Publish messages can be to/from Client/Server
