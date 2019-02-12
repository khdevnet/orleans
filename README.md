# Orleans
Orleans provides an intuitive way of building a stateful middle tier, where various business logic entities appear as sea of isolated globally addressable .NET objects (**grains**) of different application defined types distributed across a cluster of servers (**silos**).

![](https://github.com/khdevnet/orleans/blob/master/docs/orleans-basic-architecture.png)
* **Orleans** - framework for building distributed systems, high scale, low latency, high availability.
* **Grains** - A grain type is a simple .NET class that implements one or more application-defined grain interfaces. Individual grains are instances of application-defined grain classes that get automatically created by the Orleans runtime on servers on an as-needed basis to handle requests for those grains. Grains naturally map to most application entities, such as users, devices, sessions, inventories, and orders. 
* **Silos** - host grains (acivate/diactivate them), manage grains lifecycle, designed to work like a cluster
* **Stateless Worker grains** - When the [StatelessWorker] attribute is applied to a grain class, it indicates to the Orleans runtime that grains of that class should be treated as Stateless Worker grains. Stateless Worker grains have the following properties that make their execution very different from that of normal grain classes.
 * **Reentrant Grains** a reentrant activation may start executing another request while a previous request has not finished processing and has pending closures.
 ![](https://github.com/khdevnet/orleans/blob/master/docs/orleans-grains-communication.png)
* **immutable** - When a grain method is invoked, the Orleans runtime makes a deep copy of the method arguments and forms the request out of the copies. This protects against the calling code modifying the argument objects before the data is passed to the called grain.
If the called grain is on a different silo, then the copies are eventually serialized into a byte stream and sent over the network to the target silo, where they are deserialized back into objects. If the called grain is on the same silo, then the copies are handed directly to the called method.
* **Timers** are used to create periodic grain behavior that isn't required to span multiple activations (instantiations of the grain). It is essentially identical to the standard .NET System.Threading.Timer class. 
* **Reminders** are persistent and will continue to trigger in all situations (including partial or full cluster restarts) unless explicitly cancelled. If a grain has no activation associated with it and a reminder ticks, one will be created.  Reminders should not be used for high-frequency timers-- their period should be measured in minutes, hours, or days.
