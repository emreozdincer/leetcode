### CAP Theorem

In a distributed computer system, you can only support two of the following guarantees:

* Consistency - Every read receives the most recent write or an error
* Availability - Every request receives a response, without guarantee that it contains the most recent version of the information
* Partition Tolerance - The system continues to operate despite arbitrary partitioning due to network failures

*Networks aren't reliable, so you'll need to support partition tolerance. You'll need to make a software tradeoff between consistency and availability.*

**CP - consistency and partition tolerance**

Waiting for a response from the partitioned node might result in a timeout error. CP is a good choice if your business needs require atomic reads and writes.

**AP - availability and partition tolerance**

Responses return the most readily available version of the data available on any node, which might not be the latest. Writes might take some time to propagate when the partition is resolved.

AP is a good choice if the business needs allow for eventual consistency or when the system needs to continue working despite external errors.

### Consistency Patterns

With multiple copies of the same data, we are faced with options on how to synchronize them so clients have a consistent view of the data. Recall the definition of consistency from the CAP theorem - Every read receives the most recent write or an error.

**Weak Consistency**: After a write, reads may or may not see it. A best effort approach is taken.

This approach is seen in systems such as memcached. Weak consistency works well in real time use cases such as VoIP, video chat, and realtime multiplayer games. For example, if you are on a phone call and lose reception for a few seconds, when you regain connection you do not hear what was spoken during connection loss.

**Eventual Consistency**: After a write, reads will eventually see it (typically within milliseconds). Data is replicated asynchronously.

This approach is seen in systems such as DNS and email. Eventual consistency works well in highly available systems.

**Strong consistency**: weAfter a write, reads will see it. Data is replicated synchronously.

This approach is seen in file systems and RDBMSes. Strong consistency works well in systems that need transactions.

### CDNs

Push vs pull CDNS. 

* Push CDN: Updates whenever content changes on original server.  Content is uploaded only when it is new or changed, minimizing traffic, but maximizing storage. Sites with a small amount of traffic or sites with content that isn't often updated work well with push CDNs. Content is placed on the CDNs once, instead of being re-pulled at regular intervals.
* Pull CDN: CDN pulls data from server, on request of user, if data isn't already available in the CDN. Utilizes TTL. Pull CDNs minimize storage space on the CDN, but can create redundant traffic if files expire and are pulled before they have actually changed. Sites with heavy traffic work well with pull CDNs, as traffic is spread out more evenly with only recently-requested content remaining on the CDN.

### Load Balancers

* Layer 4 based routing: transport layer
* Layer 7 based routing: application layer: video data to video server, billing data to secure server etc.
* Aside from obvious ones, an advantage is SSL termination: Decrypt incoming requests and encrypt server responses so backend servers do not have to perform these potentially expensive operations
* Disadv. of horizontal scaling: increased complexity (handle more caching, connections), state/session management

### Reverse Proxy

* A reverse proxy is a web server that centralizes internal services and provides unified interfaces to the public. Requests from clients are forwarded to a server that can fulfill it before the reverse proxy returns the server's response to the client.
* RP vs LB: RP can be helpful even if you have a single server by providing security, scalability, speed benefits. They are similar things though. 
* If you only have a single RP, you introduce a SoP. If you have multiple, you introduce complexity.

### Monolith vs Microservices

* Easier to develop monolith apps at the start. Easier to deploy and test monolith at the start.
* As product evolves, monolith starts being more of an hinderance rather than a convenience. Development gets very hard. Whole system may fail when there is a single bug. Complexity introduces longer system restart or maintanance. Hard to make small updates, as the whole system needs to update.
* Microservices are more scalable. Easier to develop indivudual modules with different teams. Everyone can know about different parts of system and it will be fine.
* Microservices introduce a different set of problems: the APIs become important as different services depend on them. End-to-end or integration tests get harder to execute as you need to spin up every single relevant microservice. CI/CD can decrease this problem to an extent.
