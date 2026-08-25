## Introduction, Layers of the Internet

The Internet transfers data between computers.

- Laptops, phones, tablets, car navigators, pacemakers, etc.

The Internet has and is transforming everything.

The Internet is federated.

- No single operator. Over 100,000 different network operators!

- Operators most cooperate to form a global network.

- Must consider business incentives.

- Complicates innovation.
  
  - Operators have to run the same software to talk to each other.
  
  - If you have a brand-new feature, but nobody else has it, it's useless.

The Internet is scalable.

- Billions of users, accessing trillions of web pages.

The Internet is constantly evolving.

- Demand is constantly increasing!

The Internet is diverse.

- Some users download more data than others.

- Some devices are higher-capacity than others.

The Internet is asynchronous.

- We're constrained by the speed of light.

- Any data we receive is already dated.

The Internet is all over the world. So it's not the case that when you update something, someone else gets the update right away. There's a speed limit in physics called the speed of light. Things cannot travel faster than the speed of light. So what that means is, for example, if I update something here in San Francisco, by the time it reaches New York, even if it travels at the fastest possible speed with no obstacles along the way, it would still take thirteen milliseconds. Thirteen milliseconds is actually a really long time in computer world. And if you have a CPU that runs at this particular frequency, that means that your CPU has already executed 42 million instructions by the time your message has reached New York. By the time you get the information, you have already done lots of other work, and the information that you receive is outdated. There's just no way to get instant updates from New York because it's too far away.

The Internet must handle failures at scale.

- Sending a message requires many components (wires, network devices, software).

- Asynchrony: Might take a long time to hear the bad news.

- The Internet was the first system that had to handle failure at scale!

We have no theoretical model or performance benchmark.

- The Internet is not "optimal" according to any metric.

- But it balances lots of different goals very well.

- Need to think about practical trade-offs.

Writing code that works is not enough.

- Code must respect companies' business incentives.

- Code must run at enormous scale.

The Internet is all about designing ***protocols***.

Protocol: A specification on how to communicate.

Designing a good protocol is harder than it first seems. The IETF (Internet Engineering Task Force) standardizes and publishes protocols in RFC (Request For Comments) documents.

We need some physical technology to move bits across space.

- Voltages on electrical wire.

- Light signals on optical fiber.

- Wireless radio waves.

The Internet is a network of networks.

- Each operator runs its own local network.

- The local networks connect to each other to form the Internet.

End hosts are the machines communicating over the Internet.

Switches (aka routers) receive packets and forward them toward their destination.

Modularity: In our design, we decomposed the system into layers of abstraction.

- Each layer relies on services from the layer below.

- Each layer provides services to the layer above.

Abstraction is very powerful. Layers of abstraction are great. They allow me to hide lower level details that I don't need. And when we built the Internet, we also built it with layers of abstraction.

| Layer 3:     | Internet     | Connect many local networks to form the Internet. |
|:------------:|:------------:|:-------------------------------------------------:|
| **Layer 2:** | **Link**     | **Create links in a local network.**              |
| **Layer 1:** | **Physical** | **Move bits across space.**                       |

A packet can take multiple hops to reach its destination.

- Each router needs to forward the packet closer to its destination.

A packet can travel across multiple networks to reach its destination.

- Each local network along the way could use a different Layer 2 protocol.

Layer 3 offers a best-effort service model.

- Packets are limited in size.

- Packets could get lost, reordered, corrupted, etc.

- The network will try its best to deliver your packet, but no guarantee.

- The network won't tell you if the delivery failed.

We need to build more layers if we want to guarantee packet delivery.

***Transport*** layer builds on top of Layer 3 (global packet delivery).

- Adds extra mechanisms (e.g. re-sending lost packets) for reliable packet delivery.

- Splits up large data into packets to send them. Reassembles received packets.

- Instead of individual packets, can think about ***flows*** (aka ***connections***): A stream of packets exchanged between two endpoints.

| Layer 4:     | Transport    | Reliably deliver packets, forming connections.        |
|:------------:|:------------:|:-----------------------------------------------------:|
| **Layer 3:** | **Internet** | **Connect many local networks to form the Internet.** |
| **Layer 2:** | **Link**     | **Create links in a local network.**                  |
| **Layer 1:** | **Physical** | **Move bits across space.**                           |

***Application*** layer builds services (e.g. websites, video streaming) on top of Layer 4.

- This design lets us build different services, all on the same infrastructure.

*Note: Layers 5 and 6 are now obsolete.*

| Layer 7:     | Application   | Implement services on top of the Internet infrastructure. |
|:------------:|:-------------:|:---------------------------------------------------------:|
| **Layer 4:** | **Transport** | **Reliably deliver packets, forming connections.**        |
| **Layer 3:** | **Internet**  | **Connect many local networks to form the Internet.**     |
| **Layer 2:** | **Link**      | **Create links in a local network.**                      |
| **Layer 1:** | **Physical**  | **Move bits across space.**                               |

**Why Do We Need Headers?**

Suppose A wants to send an image to B.

- A forms a packet with the bits of the image. (May need to split image into multiple packets.)

- A sends the packet to the next router.

- The router has no idea what these bits are for!

The packet needs some extra ***metadata***, to tell us what to do with the packet.

**Common Header Fields**

The packet header contains metadata describing how the data should be sent.

Some common fields in a header:

- Destination address: Required to deliver the packet.

- Source address: Useful if the recipient wants to send replies back.

The actual data in the packet is called the ***payload***.

Headers are standardized. Everybody needs to agree on the format of the header. If we use a different format, others won't understand the header.

**Implementing Layers at Routers and End Hosts**

End hosts implement all the layers.

- Must take message, and wrap headers all the way down to bits on the wire.

Routers only implement Layers 1-3.

- Must parse the packet (1,2) and forward to the next router for global delivery (3).

- Routers don't support reliable delivery (4).

- Routers don't care about the application data (7).

**Multiple Headers with Routers**

Routers unwrap the Layer 2 header, and add a new Layer 2 header for the next hop.

Different layers use different addressing schemes.

- Each addressing scheme only makes sense to the protocol at that layer.

*Layer 2 header: Destination is the next intermediate router.*

*Layer 3 header: Destination is always the end host.*

*Layer 4 header: Identifies specific application on the end host.*

Routers don't care about Layer 4 and Layer 7.

Router parses Layers 1-3 to determine where to forward the packet.

Router unwraps Layer 2 header, and adds a new Layer 2 header for the next hop.

Each hop could use a different Layer 2 protocol.

---

## Internet Design Principles

The Internet poses a unique design challenge.

Many new paradigms emerged from the design of the Internet.

- A radical departure from systems at the time.

- Now routinely adopted in modern systems (e.g. cloud services).

These paradigms shaped how we reason about designing complex systems.

- What's the right prioritization of goals?

- What are the fundamental constraints?

- How do we decompose a problem?

- What abstractions do we need?

- What are the tradeoffs?

The Internet is a lesson in how to architect a networked system.

The Internet Design Principles:

1. Decentralized control.
   
   - Each network device (e.g. router) runs on its own. No central mastermind.
   
   - Alternative: SDN (Software-Defined Networking) centralizes control for performance.
   
   - Alternative: DSDN (Distributed SDN) moves back toward decentralization again!

2. Best-effort service model.
   
   - At Layer 3, routers only offer best-effort delivery.
   
   - Alternative: Could introduce some "quality-of-service" guarantees.

3. Route around trouble.
   
   - Network must be resilient to failures.
   
   - If a router or line goes down, find a different path through the network.

4. Dumb infrastructure (with smart endpoints).
   
   - Routers forward packets. They don't care about what's inside.
   
   - Alternative: Routers look inside payloads to help detect attacks.

5. End-to-end principle.
   
   - Implement features at the end hosts, not at the routers.

6. Layering.
   
   - Each layer relies on the layer below, and supports the layer above.
   
   - Allows us to innovate at one layer, without disturbing other layers.
   
   - Different communities can work on different layers.
     
     - Chip designers at Layers 1 and 2.
     
     - Application developers at Layer 7.
   
   - Alternative: Protocols spanning multiple layers let us optimize several layers together.

7. Federation via narrow-waist interface.
   
   - Federation works because all operators speak the same Layer 3 protocol.

These are guidelines, not unbreakable rules.

***End-to-end principle***: Certain application features (e.g. reliability) must be implemented at the end host for correctness.

The end-to-end principle is not an unbreakable rule.

- Could implement reliability in the network as a performance optimization.

- Must be done in addition to end-to-end checks, for correctness.

- Need for this must be evaluated on a case-by-case basis.

> "The function in question can completely and correctly be implemented only with the knowledge and help of the application at the end points.
> 
> Therefore, providing that function as a feature of the communication system itself is not possible.
> 
> Sometimes an incomplete version of the function provided by the communication system may be useful as a performance enhancement."

**Sharing Network Resources**

The network must support many simultaneous flows.

- A flow is a stream of packets sent between two end hosts.

- This means network resources are shared between end hosts.

Two ways to allocate resources to users:

- Static allocation: Give a fixed amount to each user.

- Statistical multiplexing: Dynamically allocate to users based on their demand.

Network resources are ***statistically multiplexed***.

Statistical multiplexing (dynamic) is more efficient than static allocation (fixed).

- Fixed: You have to give everyone enough for their peak demand.

- Dynamic: Give a user more when their demand peaks.

peak of aggregate demand < aggregate of peak demands

$$
max(\sum f_i)<\sum max(f_i)
$$

In practice, peak of aggregate is usually closer to the average of peak demands.

There are 2 canonical designs for implementing statistical multiplexing:

- ***Reservations*** via circuit switching:
  
  - At start of connection, end-hosts explicitly request and reserve resources.
  
  - During connection, use the reserved resources to send packets.
  
  - At end of connection, release resources.

- ***Best-effort*** via packet switching:
  
  - Just use the resources (send packets) and hope for the best.

As a programmer, circuit switching is more convenient.

- You get a guarantee of reserved resources.

- More predictable and understandable behavior.

- Leads to an intuitive business model for companies.
  
  - Charge a user depending on what they reserve.

Packet switching is typically more efficient.

- Circuit switching takes time for setup/teardown.
  
  - Very inefficient if you don't have much data to send, e.g. short flows.

- Circuit switching can lead to wasted resources.

Circuit switching with bursty traffic leads to inefficient resource allocation.

Flows can be smooth or bursty.

- Characterized by the ratio between the flow's peak demand and average demand.

- Smooth applications have a small peak-to-average ratio.
  
  - Voice has a ratio of ~3:1. This is why the phone network uses reservations!

- Bursty applications have a large peak-to-average ratio.
  
  - Data applications tend to be rather bursty.
  
  - Web browsing can have a ratio of 100:1 or more.
