# Orleans
Orleans provides an intuitive way of building a stateful middle tier, where various business logic entities appear as sea of isolated globally addressable .NET objects (**grains**) of different application defined types distributed across a cluster of servers (**silos**).

![](https://github.com/khdevnet/orleans/blob/master/docs/orleans-basic-architecture.png)
* **Orleans** - framework for building distributed systems, high scale, low latency, high availability.
* **Grains** - A grain type is a simple .NET class that implements one or more application-defined grain interfaces. Individual grains are instances of application-defined grain classes that get automatically created by the Orleans runtime on servers on an as-needed basis to handle requests for those grains. Grains naturally map to most application entities, such as users, devices, sessions, inventories, and orders. 
* **Silos** - host grains (acivate/diactivate them), manage grains lifecycle, designed to work like a cluster
* **Stateless Worker grains** - When the [StatelessWorker] attribute is applied to a grain class, it indicates to the Orleans runtime that grains of that class should be treated as Stateless Worker grains. Stateless Worker grains have the following properties that make their execution very different from that of normal grain classes.
 * **Reentrant Grains** a reentrant activation may start executing another request while a previous request has not finished processing and has pending closures. 
