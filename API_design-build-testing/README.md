# API: Designing, Building and Testing

- [API: Designing, Building and Testing](#api-designing-building-and-testing)
  - [Bibliografia](#bibliografia)
  - [What is an API](#what-is-an-api)
  - [REST](#rest)
    - [Richardson Maturity Heuristics](#richardson-maturity-heuristics)
      - [Level 0](#level-0)
      - [Level 1](#level-1)
      - [Level 2](#level-2)
      - [Level 3](#level-3)

## Bibliografia

- https://www.redhat.com/en/topics/api/what-are-application-programming-interfaces
- "Mastering API Architecture, Design, Operate and Evolve API-Based Systems" J. Gough, D. Bryant, M. Auburn (2021) O'Reilly
- https://www.ics.uci.edu/~fielding/pubs/dissertation/top.htm

## What is an API

API stants for application programming interface, which is a set of definitions and protocols for building and integrating application software

APIs let a product or service communicate with other products and services without having to know how they are implemented. This can simplify ap development.

- Represents an abstraction of the underlying implementation
- Is represented by a specification that introduces types.
- Has defined semantics or behavior to effectivelly model the exchange of information
- Enables extension to customers or third parties for a business integration

## REST

Representation State Transfer (REST) is a set of architectural constraints, most commonly appplied using HTTP as the underlying transport protocol. From a practical perspective, a RESTful API must ensure that:

- A producer-to-consumer interaction is modeled where the producer models resources the consumer can interact with
- Requests from producer to consumer are stateless, meaning that the producer does not cache details of a previous request
- Requests are cachable, meaning the producer can providehits to the consumer where is appropiate.
- A uniform interface is conveyed to the consumer.
- It is a layered system, abstracting away the complexity of systems sitting behind the REST interface.

### Richardson Maturity Heuristics

#### Level 0

- **HTTP/RCP** Establishes that the API is built using HTTP and has the notion of a single URI. This represents an RCP implementation over the REST protocol

#### Level 1

- **Resources:** Establishes the use of resources and starts to bring in the idea of modeling resources in the context of the URI.

#### Level 2

- **Verbs** Guarantees around emehthods not impacting server state and presenting multiple operations on the same resource URI. 

#### Level 3 

- **Hypermedia Controls** In practical terms level 3 is rarely used in modern RESTful HTTP services. Uses the HATEOAS Hypertext As The Engine Of Application State


