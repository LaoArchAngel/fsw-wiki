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

Each event available by a team should be documented in at least two separate
locations: the documentation of the software that is generating the event,
and a document listing all events that the team is publishing.

## Exchange

The Exchange is like the
[Event](https://msdn.microsoft.com/en-us/library/8627sbea%28v=vs.120%29.aspx)
in C# and .NET. It tells all listening delegates that the event was called and
provides all associated data.

An Exchange is how each team will "publish" their events to other teams. Each
exchange will be bound to one or more queues, depending on the different teams
or applications that are interested in an event published through the exchange.

Each team should have at least one exchange for events. It will make more
sense for each bounded context, and sometimes one for each application. These
event Exchanges cannot be Direct, as multiple queues should be able to accept
events from a single exchange.

Different types of events are available depending on the type of event
filtering available to the consuming queues.

### Fan-Out Exchange

**Fan-Out Exchanges** are useful when you want every queue listening to the
exchange to process the same event. The usefulness of this type of exchange is
limited to single or simple event streams.

### Header Exchange

**Header Exchanges** provide the most filtering capability but also the most
complexity. Header exchanges will be useful when dealing with a large number
of events or a large volume of the same type of event. Providing filterable
information in the header of the event message would allow queues to accept
only the events in which its consumers are interested.

### Topic Exchange

**Topic Exchanges** are useful when events only need to be filtered by name.
For example, if an event is named _ProductNameChange_, queues can choose to
accept it based on the name, but no other criteria. This is useful when
dealing with a manageable number of events.
