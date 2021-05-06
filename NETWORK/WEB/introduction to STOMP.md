# STOMP

> Simple(or Streaming) Text Orientated Messaging Protocol
>
> = 간단한 텍스트 기반 메세징 프로토콜

- a simple and easy to implement protocol

- designed for asynchronous message passing between clients via mediating servers

- a text based *wire format* for messages passed between clients and servers

  - wire protocol : a way of getting data from point to point. needed if more than one application has to inter-operate.

- supported by several *message brokers*

  - message broker: an intermediary computer program module that translates messages between sender and receiver based on their messaging protocols 
    - sender (A protocol) ==> message broker ==> receiver (B protocol)

- `frame` based protocol (frames based on HTTP models)

  - a frame consists of `command`, `headers`, `body`

  ```
  COMMAND
  header1:value1
  header2:value2
  
  Body^@
  ```