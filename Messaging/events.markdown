# Events
This document describes the process of using [RabbitMQ](Messaging/RabbitMQ) as
an event bus.

## Overview

* Exchange
  * Fan-Out
    * When a team wants to publish events and plans to let consumers manage
    which events they consume on their end.
  * Headers
    * When a team wants to publish events with complex event information in
    the header to allow for more granular filtering of events.
  * Topic
    * When a team wants to publish multiple different related events and let
    listening queues filter by event name. (eg. ProductNameUpdate,
    ProductDescUpdate)

## Preparation

All events should be saved in database storage prior to being published.
This will ensure that any events can be replayed in the future in case of
catastrophic failure.
