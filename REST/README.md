# Representational State Stransfer 

- [Representational State Stransfer](#representational-state-stransfer)
  - [Introduction](#introduction)
    - [Hypermedia](#hypermedia)
    - [Client-Server (CS)](#client-server-cs)
    - [Client-Stateless-Server (CSS)](#client-stateless-server-css)
    - [Client-Cache-Stateless-Server (C$SS)](#client-cache-stateless-server-css)
    - [Layered System and Layered-Client-Server (LCS)](#layered-system-and-layered-client-server-lcs)
    - [Code on Demand (COD)](#code-on-demand-cod)
  - [REST](#rest)
  - [REST Architectural Elements](#rest-architectural-elements)
    - [Data Elements](#data-elements)
      - [REST Data Elements](#rest-data-elements)
    - [Connectors](#connectors)

## Introduction

### Hypermedia

Hypermedia, an extension of the term hypertext, is a nonlinear medium of information that includes graphics, audio, video, plain text and hyperlinks. The WWW is a example of hypermedia to access web content.

### Client-Server (CS)

- Most frequently encoundered of the architectural styles for network-based applications. 
- A server component offers a set of services, listen for requests upon those services (reactive process)
- A client component, send requests to the server via a **connector** (triggering process)
- The server rejects or performs the request and sends a response back to the client 
- Separation of concerns is the principole  echind client-server constraints

### Client-Stateless-Server (CSS)

Derives from client-server with the additional constraint that **no session state** is allowed on the server component.

- Each request from client to server must contain all of the information necessary to understand the request.
- Cannot take advantage of any stored context on the server
- Session state is kept entirely on the client

These constraints improve **visibility, reliability** and **scalability**. Teh disadvantage of CSS is that it may decrease network performance by increasing the repetitive data, since the data cannot be left on the server in a shared context.

### Client-Cache-Stateless-Server (C$SS)

Derives from client-stateless-server and cache styles via addition of cache components. cache acts as a mediator between client and server. 

The advantage of adding cache components is that they have the potential to partially or completely eliminate some interactions, improving efficiency and user-perceived performance.

### Layered System and Layered-Client-Server (LCS)

A layered system is organized hierarchically, each layer providing services to the layer above it and using services of the layer below it.

LAyered systems reduce coupling across multiple layers by hiding the inner layers from all except the adjacent outer layer. thus improving evolvability and reusabilityh. 

The primary disadvantage of layered systems is that they add overhead and latency to the processing of data, reducing user perceived performance.

LCS adds proxy and gateway components to the client-server sttyle. A proxy acts as a shared server for one or more client components, taking requests and forwarding them, with possible translation, to server components. A gateway component appears to be a normal server to clients or proxies that request its services, but is in fact forwarding those requests, with possible translation to its "inner-layer" servers. These additional mediator components can be added in multiple layers to add features like load balancing and security checking to the system.

LCS is a solution to managing identity in a large scale distributed syhstem. Where complete knowledge of all servers would be prohibitively expensive, instead servers are organized in layers such that rarely used services are handled by intermediaries rather tha direcly by each client.

### Code on Demand (COD)

In a COD style a client has access to a set of resources, but not the know-how on how to process them. It sends a request to a remote server receiving that code and executes it locally.



## REST

From a architectural design process, we start from the system needs as a whole, without constraints, and the nincrementally identifies and applies contraints to elements of the system in order to differentiate the design space.

0. **Null State:** From an architectural perspective, the null style describes a system in which there are no distinguished boundaries between components. It is the starting point for our description of REST

2. **Client-Server**: First constraints added to hybrid style are client-server. By separating the UI concerns from the DATA-STORAGE concerns, we improve the portability of the user interface across multiple platforms and improve scalability by simplifying the server components.

3. **Stateless:** Communication must be stateless in nature, as in the CSS style. Each request from client to server must contain all the information necccessary to understand the request. We improve realiability, scalability and visibility. The disadvantage is that it may decrease network performance by increasing repetitive data.

4. **Cache**: To improve network efficiency, cache constraints require that the data within a response to a request be implicitly or explicitly labeled as cacheable or non-cacheable. If a response is cacheable, then a client cache is given the right to reuse that response data for later, equivalent requests.

5. **Uniform Interface** The central feature that distinguishes the REST architectural style from other network-based styles is its emphasis on a uniform interface between components. The REST interface is designed to be efficient for large-grain hypermedia data transfer, optimizing for the common case of the Web, but resulting an interface that is not optimal forother forms of architectural interaction. 

Rest is defined by four interface constriants

- identification of resources
- manipulation of resources through representations
- self-descriptive messages
- hypermedia as the engine of the application state

6. **Layered System**: To improve behavior, add a layered system constraints. LCS allows an architecture to be composed of layers by constraining component behavior such that each component cannot see beyond the immediate layer with which they are interacting.

The primary disadvantage of layered systems is that they add overhead and latency to the processing of data, reducing user-perceived performance. For a network-based system that supports cache constraints. this can be offset by the benefits of shared caching at intermediaries. Layers allow security policies,.

7. **Code-On-Demand** REST allows client functionality to be extended by downloading and executing code in the form of applets or scripts. This simplifies clients by reducing the number of features required to be pre-implemented. Allowing features to be downloaded after deployment improves system extensibility.

This is an optional constraint. 

## REST Architectural Elements 

REST ignores the details of component implementation and protocol syntax in order to focus on the roles of components, the constraints upon their interaction with other components, and their interpretation of significant data elements.

### Data Elements

When a link is selected, information needs to eb moved from the location where it is stored to the location where it will be used. 

An architect has three fundamental options:

1. Render the data where it is located and send a fixed-format image to the recipient (traditional client-server style) 
    - Allows all info about the nature of the data to remain hidden within the sender, preventing assuptions
    - Restrictis reverely the functionality of the recipient and places the processing load on the sender, leading to scalability problems
2. Encapsulate the data with a rendering engine and send both to a recipient
  - limits the funcitonality of the recipient
3. Send the raw data to the recipient along the metadata that describes the data type, so that the recipient can choose their own rendering engine 
   - Allows the sender to remain simple and scalable while minimizing the bytes transferred
   - Loses the advantages of information hiding and requires that both understand the same data types

#### REST Data Elements

Data Element | Modern Web Example
-- | -- 
resource identifier | URL
representation | HTML document, JPEG image
representation metadata | media type
resource metadata | source link
control data | cache control

### Connectors 

The connectors present an abstract interface for component communication, enhancing siplicty by providing a clean separation of concerns and hiding the underlying implementation of resources and communication mechanisms.

If the users only acccess to the system via an abstract interface, the implementation can be replaced without impacting the users. Since a connector manages network communication for a component, information can be shared across multiple interactions in order to improve efficiency and responsiveness.

Conector | Web Example
-- | -- 
client | perl 
server | Apache, Nginx 
cache | browser cache 
resolver | DNS 
tunnel | SSL after HTTP

- All rest interactions are stateless

The primary conector types are client and server. The client initiates communication by making a request, where as server listens for connections and responds to requests in order to supply access to its services.

A third connector type, cache connector, can be located on the interface to a client or server connector in order to save cacheable responses to current interactions. A cache may be used by a client to avoid repetition of network communiaction, or by a server to avoid repeating the process of generating a response. Both cases serving to reduce interaction latency.

Some cache connectors are shared. Shared caching can be effective at reducing the impact on the load of a popular server.

A resolver translates partial or complete resource identifiers into the network addres information needed to establish an inter-component connection. For example, most URI include a DNS hostname as the mechanism for identifying the naming authority for the resource. In order to initiate a request, a Web browser will extract the hostname from the URI and make use of a DNS resolver to obtain te Internet Protocol address for that authority. 

The ifnal form of connector type is a tunnel, which relays communication across a connection boudary, such as a fireall or lower level network gateway. Some REST components may dynamically witch from active component behavior toe that of a tunnel. The primary example is an HTTP proxy that switches to a tunnel in response to a CONNECT method request.