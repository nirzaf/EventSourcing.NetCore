# EventSourcing .NET

- [EventSourcing .NET](#eventsourcing-net)
  - [1. Event Sourcing](#1-event-sourcing)
    - [1.1 What is Event Sourcing?](#11-what-is-event-sourcing)
    - [1.2 What is Event?](#12-what-is-event)
    - [1.3 What is Stream?](#13-what-is-stream)
    - [1.4 Event representation](#14-event-representation)
    - [1.5 Event Storage](#15-event-storage)
    - [1.6 Retrieving the current state from events](#16-retrieving-the-current-state-from-events)
    - [1.7 Strongly-Typed ids with Marten](#17-strongly-typed-ids-with-marten)
  - [2. Videos](#2-videos)
    - [2.1. Practical Event Sourcing with Marten](#21-practical-event-sourcing-with-marten)
    - [2.2. Practical Introduction to Event Sourcing with EventStoreDB](#22-practical-introduction-to-event-sourcing-with-eventstoredb)
    - [2.3 Let's build the worst Event Sourcing system!](#23-lets-build-the-worst-event-sourcing-system)
    - [2.4 The Light and The Dark Side of the Event-Driven Design](#24-the-light-and-the-dark-side-of-the-event-driven-design)
    - [2.5 Conversation with Yves Lorphelin about CQRS](#25-conversation-with-yves-lorphelin-about-cqrs)
    - [2.6. CQRS is Simpler than you think with C#9 & NET5](#26-cqrs-is-simpler-than-you-think-with-c9--net5)
    - [2.7. Never Lose Data Again - Event Sourcing to the Rescue!](#27-never-lose-data-again---event-sourcing-to-the-rescue)
    - [2.8. How to deal with privacy and GDPR in Event-Sourced systems](#28-how-to-deal-with-privacy-and-gdpr-in-event-sourced-systems)
  - [3. Support](#3-support)
  - [4. Prerequisites](#4-prerequisites)
  - [5. Tools used](#5-tools-used)
  - [6. Samples](#6-samples)
    - [6.1 Pragmatic Event Sourcing With Marten](#61-pragmatic-event-sourcing-with-marten)
    - [6.2 ECommerce with Marten](#62-ecommerce-with-marten)
    - [6.3 Simple EventSourcing with EventStoreDB](#63-simple-eventsourcing-with-eventstoredb)
    - [6.4 ECommerce with EventStoreDB](#64-ecommerce-with-eventstoredb)
    - [6.5 Warehouse](#65-warehouse)
    - [6.6 Warehouse Minimal API](#66-warehouse-minimal-api)
    - [6.7 Event Versioning](#67-event-versioning)
    - [6.8 Event Pipelines](#68-event-pipelines)
    - [6.9 Meetings Management with Marten](#69-meetings-management-with-marten)
    - [6.10 Cinema Tickets Reservations with Marten](#610-cinema-tickets-reservations-with-marten)
    - [6.11 SmartHome IoT with Marten](#611-smarthome-iot-with-marten)
  - [7. Self-paced training Kits](#7-self-paced-training-kits)
    - [7.1 Introduction to Event Sourcing](#71-introduction-to-event-sourcing)
    - [7.2 Build your own Event Store](#72-build-your-own-event-store)
  - [8. Articles](#8-articles)
  - [9. Event Store - Marten](#9-event-store---marten)
  - [10. Message Bus (for processing Commands, Queries, Events) - MediatR](#10-message-bus-for-processing-commands-queries-events---mediatr)
  - [11. CQRS (Command Query Responsibility Separation)](#11-cqrs-command-query-responsibility-separation)
  - [12. NuGet packages to help you get started.](#12-nuget-packages-to-help-you-get-started)
  - [13. Other resources](#13-other-resources)
    - [13.1 Introduction](#131-introduction)
    - [13.2 Event Sourcing on production](#132-event-sourcing-on-production)
    - [13.3 Projections](#133-projections)
    - [13.4 Snapshots](#134-snapshots)
    - [13.5 Versioning](#135-versioning)
    - [13.6 Storage](#136-storage)
    - [13.7 Design & Modeling](#137-design--modeling)
    - [13.8 GDPR](#138-gdpr)
    - [13.9 Conflict Detection](#139-conflict-detection)
    - [13.10 Functional programming](#1310-functional-programming)
    - [13.12 Testing](#1312-testing)
    - [13.13 CQRS](#1313-cqrs)
    - [13.14 Tools](#1314-tools)
    - [13.15 Event processing](#1315-event-processing)
    - [13.16 Distributed processes](#1316-distributed-processes)
    - [13.17 Domain Driven Design](#1317-domain-driven-design)
    - [13.18 Whitepapers](#1318-whitepapers)
    - [13.19 This is NOT Event Sourcing (but Event Streaming)](#1319-this-is-not-event-sourcing-but-event-streaming)
    - [13.20 Event Sourcing Concerns](#1320-event-sourcing-concerns)
    - [13.21 Architecture Weekly](#1321-architecture-weekly)


## 1. Event Sourcing

### 1.1 What is Event Sourcing?

Event Sourcing is a design pattern in which results of business operations are stored as a series of events.

It is an alternative way to persist data. In contrast with state-oriented persistence that only keeps the latest version of the entity state, Event Sourcing stores each state change as a separate event.

Thanks to that, no business data is lost. Each operation results in the event stored in the database. That enables extended auditing and diagnostics capabilities (both technically and business-wise). What's more, as events contains the business context, it allows wide business analysis and reporting.

In this repository I'm showing different aspects and patterns around Event Sourcing from the basic to advanced practices.

Read more in my articles:
-   📝 [How using events helps in a teams' autonomy](https://event-driven.io/en/how_using_events_help_in_teams_autonomy/?utm_source=event_sourcing_net)
-   📝 [When not to use Event Sourcing?](https://event-driven.io/en/when_not_to_use_event_sourcing/?utm_source=event_sourcing_net)

### 1.2 What is Event?

Events represent facts in the past. They carry information about something accomplished. It should be named in the past tense, e.g. _"user added"_, _"order confirmed"_. Events are not directed to a specific recipient - they're broadcasted information. It's like telling a story at a party. We hope that someone listens to us, but we may quickly realise that no one is paying attention.

Events:
- are immutable: _"What has been seen, cannot be unseen"_.
- can be ignored but cannot be retracted (as you cannot change the past).
- can be interpreted differently. The basketball match result is a fact. Winning team fans will interpret it positively. Losing team fans - not so much.

Read more in my articles:
-   📝 [What's the difference between a command and an event?](https://event-driven.io/en/whats_the_difference_between_event_and_command/?utm_source=event_sourcing_net)
-   📝 [Events should be as small as possible, right?](https://event-driven.io/en/events_should_be_as_small_as_possible/?utm_source=event_sourcing_net)
-   📝 [Anti-patterns in event modelling - Property Sourcing](https://event-driven.io/en/property-sourcing/?utm_source=event_sourcing_net)
-   📝 [Anti-patterns in event modelling - State Obsession](https://event-driven.io/en/state-obsession/?utm_source=event_sourcing_net)

### 1.3 What is Stream?

Events are logically grouped into streams. In Event Sourcing, streams are the representation of the entities. All the entity state mutations end up as the persisted events. Entity state is retrieved by reading all the stream events and applying them one by one in the order of appearance.

A stream should have a unique identifier representing the specific object. Each event has its own unique position within a stream. This position is usually represented by a numeric, incremental value. This number can be used to define the order of the events while retrieving the state. It can also be used to detect concurrency issues.

### 1.4 Event representation

Technically events are messages.

They may be represented, e.g. in JSON, Binary, XML format. Besides the data, they usually contain:
- **id**: unique event identifier.
- **type**: name of the event, e.g. _"invoice issued"_.
- **stream id**: object id for which event was registered (e.g. invoice id).
- **stream position** (also named _version_, _order of occurrence_, etc.): the number used to decide the order of the event's occurrence for the specific object (stream).
- **timestamp**: representing a time at which the event happened.
- other metadata like `correlation id`, `causation id`, etc.

Sample event JSON can look like:

```json
{
  "id": "e44f813c-1a2f-4747-aed5-086805c6450e",
  "type": "invoice-issued",
  "streamId": "INV/2021/11/01",
  "streamPosition": 1,
  "timestamp": "2021-11-01T00:05:32.000Z",

  "data":
  {
    "issuedTo": {
      "name": "Oscar the Grouch",
      "address": "123 Sesame Street"
    },
    "amount": 34.12,
    "number": "INV/2021/11/01",
    "issuedAt": "2021-11-01T00:05:32.000Z"
  },

  "metadata":
  {
    "correlationId": "1fecc92e-3197-4191-b929-bd306e1110a4",
    "causationId": "c3cf07e8-9f2f-4c2d-a8e9-f8a612b4a7f1"
  }
}
```
### 1.5 Event Storage

Event Sourcing is not related to any type of storage implementation. As long as it fulfills the assumptions, it can be implemented having any backing database (relational, document, etc.). The state has to be represented by the append-only log of events. The events are stored in chronological order, and new events are appended to the previous event. Event Stores are the databases' category explicitly designed for such purpose.

Read more in my article:
-   📝 [What if I told you that Relational Databases are in fact Event Stores?](https://event-driven.io/en/relational_databases_are_event_stores/?utm_source=event_sourcing_net)

### 1.6 Retrieving the current state from events

In Event Sourcing, the state is stored in events. Events are logically grouped into streams. Streams can be thought of as the entities' representation. Traditionally (e.g. in relational or document approach), each entity is stored as a separate record.

| Id       | IssuerName       | IssuerAddress     | Amount | Number         | IssuedAt   |
| -------- | ---------------- | ----------------- | ------ | -------------- | ---------- |
| e44f813c | Oscar the Grouch | 123 Sesame Street | 34.12  | INV/2021/11/01 | 2021-11-01 |

 In Event Sourcing, the entity is stored as the series of events that happened for this specific object, e.g. `InvoiceInitiated`, `InvoiceIssued`, `InvoiceSent`.

```json
[
    {
        "id": "e44f813c-1a2f-4747-aed5-086805c6450e",
        "type": "invoice-initiated",
        "streamId": "INV/2021/11/01",
        "streamPosition": 1,
        "timestamp": "2021-11-01T00:05:32.000Z",

        "data":
        {
            "issuer": {
                "name": "Oscar the Grouch",
                "address": "123 Sesame Street",
            },
            "amount": 34.12,
            "number": "INV/2021/11/01",
            "initiatedAt": "2021-11-01T00:05:32.000Z"
        }
    },
    {
        "id": "5421d67d-d0fe-4c4c-b232-ff284810fb59",
        "type": "invoice-issued",
        "streamId": "INV/2021/11/01",
        "streamPosition": 2,
        "timestamp": "2021-11-01T00:11:32.000Z",

        "data":
        {
            "issuedTo": "Cookie Monster",
            "issuedAt": "2021-11-01T00:11:32.000Z"
        }
    },
    {
        "id": "637cfe0f-ed38-4595-8b17-2534cc706abf",
        "type": "invoice-sent",
        "streamId": "INV/2021/11/01",
        "streamPosition": 3,
        "timestamp": "2021-11-01T00:12:01.000Z",

        "data":
        {
            "sentVia": "email",
            "sentAt": "2021-11-01T00:12:01.000Z"
        }
    }
]
```

All of those events share the stream id (`"streamId": "INV/2021/11/01"`), and have incremented stream positions.

In Event Sourcing each entity is represented by its stream: the sequence of events correlated by the stream id ordered by stream position.

To get the current state of an entity we need to perform the stream aggregation process. We're translating the set of events into a single entity. This can be done with the following steps:
1. Read all events for the specific stream.
2. Order them ascending in the order of appearance (by the event's stream position).
3. Construct the empty object of the entity type (e.g. with default constructor).
4. Apply each event on the entity.

This process is called also _stream aggregation_ or _state rehydration_.

We could implement that as:

```csharp
public record Person(
    string Name,
    string Address
);

public record InvoiceInitiated(
    double Amount,
    string Number,
    Person IssuedTo,
    DateTime InitiatedAt
);

public record InvoiceIssued(
    string IssuedBy,
    DateTime IssuedAt
);

public enum InvoiceSendMethod
{
    Email,
    Post
}

public record InvoiceSent(
    InvoiceSendMethod SentVia,
    DateTime SentAt
);

public enum InvoiceStatus
{
    Initiated = 1,
    Issued = 2,
    Sent = 3
}

public class Invoice
{
    public string Id { get;set; }
    public double Amount { get; private set; }
    public string Number { get; private set; }

    public InvoiceStatus Status { get; private set; }

    public Person IssuedTo { get; private set; }
    public DateTime InitiatedAt { get; private set; }

    public string IssuedBy { get; private set; }
    public DateTime IssuedAt { get; private set; }

    public InvoiceSendMethod SentVia { get; private set; }
    public DateTime SentAt { get; private set; }

    public void When(object @event)
    {
        switch (@event)
        {
            case InvoiceInitiated invoiceInitiated:
                Apply(invoiceInitiated);
                break;
            case InvoiceIssued invoiceIssued:
                Apply(invoiceIssued);
                break;
            case InvoiceSent invoiceSent:
                Apply(invoiceSent);
                break;
        }
    }

    private void Apply(InvoiceInitiated @event)
    {
        Id = @event.Number;
        Amount = @event.Amount;
        Number = @event.Number;
        IssuedTo = @event.IssuedTo;
        InitiatedAt = @event.InitiatedAt;
        Status = InvoiceStatus.Initiated;
    }

    private void Apply(InvoiceIssued @event)
    {
        IssuedBy = @event.IssuedBy;
        IssuedAt = @event.IssuedAt;
        Status = InvoiceStatus.Issued;
    }

    private void Apply(InvoiceSent @event)
    {
        SentVia = @event.SentVia;
        SentAt = @event.SentAt;
        Status = InvoiceStatus.Sent;
    }
}
```
and use it as:

```csharp
var invoiceInitiated = new InvoiceInitiated(
    34.12,
    "INV/2021/11/01",
    new Person("Oscar the Grouch", "123 Sesame Street"),
    DateTime.UtcNow
);
var invoiceIssued = new InvoiceIssued(
    "Cookie Monster",
    DateTime.UtcNow
);
var invoiceSent = new InvoiceSent(
    InvoiceSendMethod.Email,
    DateTime.UtcNow
);

// 1,2. Get all events and sort them in the order of appearance
var events = new object[] {invoiceInitiated, invoiceIssued, invoiceSent};

// 3. Construct empty Invoice object
var invoice = new Invoice();

// 4. Apply each event on the entity.
foreach (var @event in events)
{
    invoice.When(@event);
}
```

and generalise this into `Aggregate` base class:

```csharp
public abstract class Aggregate<T>
{
    public T Id { get; protected set; }

    protected Aggregate() { }

    public virtual void When(object @event) { }
}
```

The biggest advantage of _"online"_ stream aggregation is that it always uses the most recent business logic. So after the change in the apply method, it's automatically reflected on the next run. If events data is fine, then it's not needed to do any migration or updates.

In Marten `When` method is not needed. Marten uses naming convention and call the `Apply` method internally. It has to:
- have single parameter with event object,
- have `void` type as the result.

See samples:
- [Generic stream aggregation](/Core.Tests/AggregateWithWhenTests.cs)
- [Marten](/Marten.Integration.Tests/EventStore/Aggregate/EventsAggregation.cs)
- [EventStoreDB](/Core.EventStoreDB/Events/AggregateStreamExtensions.cs)


Read more in my article:
-   📝 [How to get the current entity state from events?](https://event-driven.io/en/how_to_get_the_current_entity_state_in_event_sourcing/?utm_source=event_sourcing_net)

### 1.7 Strongly-Typed ids with Marten

Strongly typed ids (or, in general, a proper type system) can make your code more predictable. It reduces the chance of trivial mistakes, like accidentally changing parameters order of the same primitive type.

So for such code:

```csharp
var reservationId = "RES/01";
var seatId = "SEAT/22";
var customerId = "CUS/291";

var reservation = new ReservationId (
    reservationId,
    seatId,
    customerId
);
```

the compiler won't catch if you switch `reservationId` with `seatId`.

If you use strongly typed ids, then compile will catch that issue:

```csharp
var reservationId = new ReservationId("RES/01");
var seatId = new SeatId("SEAT/22");
var customerId = new CustomerId("CUS/291");

var reservation = new ReservationId (
    reservationId,
    seatId,
    customerId
);
```

They're not ideal, as they're usually not playing well with the storage engines. Typical issues are: serialisation, Linq queries, etc. For some cases they may be just overkill. You need to pick your poison.

To reduce tedious, copy/paste code, it's worth defining a strongly-typed id base class, like:

```csharp
public class StronglyTypedValue<T>: IEquatable<StronglyTypedValue<T>> where T: IComparable<T>
{
    public T Value { get; }

    public StronglyTypedValue(T value)
    {
        Value = value;
    }

    public bool Equals(StronglyTypedValue<T>? other)
    {
        if (ReferenceEquals(null, other)) return false;
        if (ReferenceEquals(this, other)) return true;
        return EqualityComparer<T>.Default.Equals(Value, other.Value);
    }

    public override bool Equals(object? obj)
    {
        if (ReferenceEquals(null, obj)) return false;
        if (ReferenceEquals(this, obj)) return true;
        if (obj.GetType() != this.GetType()) return false;
        return Equals((StronglyTypedValue<T>)obj);
    }

    public override int GetHashCode()
    {
        return EqualityComparer<T>.Default.GetHashCode(Value);
    }

    public static bool operator ==(StronglyTypedValue<T>? left, StronglyTypedValue<T>? right)
    {
        return Equals(left, right);
    }

    public static bool operator !=(StronglyTypedValue<T>? left, StronglyTypedValue<T>? right)
    {
        return !Equals(left, right);
    }
}
```

Then you can define specific id class as:

```csharp
public class ReservationId: StronglyTypedValue<Guid>
{
    public ReservationId(Guid value) : base(value)
    {
    }
}
```

You can even add additional rules:

```csharp
public class ReservationNumber: StronglyTypedValue<string>
{
    public ReservationNumber(string value) : base(value)
    {
        if (string.IsNullOrEmpty(value) || value.StartsWith("RES/") || value.Length <= 4)
            throw new ArgumentOutOfRangeException(nameof(value));
    }
}
```

The base class working with Marten, can be defined as:

```csharp
public abstract class Aggregate<TKey, T>
    where TKey: StronglyTypedValue<T>
    where T : IComparable<T>
{
    public TKey Id { get; set; } = default!;

    [Identity]
    public T AggregateId    {
        get => Id.Value;
        set {}
    }

    public int Version { get; protected set; }

    [JsonIgnore] private readonly Queue<object> uncommittedEvents = new();

    public object[] DequeueUncommittedEvents()
    {
        var dequeuedEvents = uncommittedEvents.ToArray();

        uncommittedEvents.Clear();

        return dequeuedEvents;
    }

    protected void Enqueue(object @event)
    {
        uncommittedEvents.Enqueue(@event);
    }
}
```

Marten requires the id with public setter and getter of `string` or `Guid`. We used the trick and added `AggregateId` with a strongly-typed backing field. We also informed Marten of the [Identity](https://martendb.io/documents/identity.html#document-identity) attribute to use this field in its internals.

Example aggregate can look like:

```csharp
public class Reservation : Aggregate<ReservationId, Guid>
{
    public CustomerId CustomerId { get; private set; } = default!;

    public SeatId SeatId { get; private set; } = default!;

    public ReservationNumber Number { get; private set; } = default!;

    public ReservationStatus Status { get; private set; }

    public static Reservation CreateTentative(
        SeatId seatId,
        CustomerId customerId)
    {
        return new Reservation(
            new ReservationId(Guid.NewGuid()),
            seatId,
            customerId,
            new ReservationNumber(Guid.NewGuid().ToString())
        );
    }

    // (...)
}
```
