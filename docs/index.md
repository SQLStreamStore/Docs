# Introduction

SQL Stream Store is a .NET library to assist with developing applications that use
event sourcing or wish to use stream based patterns over a relational database
and existing operational infrastructure.

This documentation assumes you already have some knowledge of event sourcing. If
not, please take a look at [Resources](resources) for interesting and relevant
links.

# Things you need to know before adopting

- This is foremost a _library_ to help with working with stream based concepts
  implemented on an RDMBS infrastructure. It has no intention of becoming a full
  blown application/database server.

- While it helps you with working with stream concepts over a relational
  databases, you must still have mechanical sympathy with the underlying
  database such as limits, log growth, performance characteristics, exception
  handling, etc. For example, this means that you need to handle any
  exceptions coming from the underlying ado.net provider.

- SQLStreamStore / relational databases will never be be as fast as custom
  stream / event based databases (e.g EventStore, Kafka). For DDD applications
  (aka "collaborative domains") that would otherwise use a traditional RDBMS
  database (and ORMs), it should perform within expectations.

- Subscriptions (and thus projections) are eventually consistent and always will
  be.

- You must understand your application's characteristics in terms of load, data
  growth, acceptable latency for eventual consistency, etc.
  
- Message metadata payloads are strings only and expected to be a JSON object literal.
  This is for operational reasons to support spelunking a database using its
  standard administration tools. Other serialization formats (or compression)
  are not supported (strictly speaking JSON isn't _enforced_ either).

- No support for ambient `System.Transaction` scopes enforcing the concept of
  the stream as the consistency and transactional boundary.
