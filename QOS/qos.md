# QoS Notes

Quality of Service (QoS) in ROS 2 is all about managing how data flows between nodes. It’s crucial because robots and distributed systems need reliable, predictable, and efficient communication. Different scenarios need different settings—some messages must be fast, some must be reliable, and some must persist even if a subscriber joins late.

### Why QoS?
- Not all messages are equally important.
- Some need **fast delivery** (like sensor data), while others need **guaranteed delivery** (like safety-critical commands).
- Ensures nodes get the right information at the right time.

## **QoS Policies**

### 1. **Reliability** (Guaranteeing Message Delivery)
Reliability defines whether messages should be guaranteed to arrive.
- **Reliable** → Ensures messages are delivered to subscribers, even if there are temporary disconnections or network issues.
- **Best Effort** → Sends messages without guarantees. If the network is bad, some messages might be lost.

### 2. **Durability** (Keeping Messages for Late Subscribers)
Durability determines if past messages should be stored when a new subscriber joins.
- **Volatile** → Only delivers messages while the publisher is active. If a subscriber connects late, it won’t receive old messages.
- **Transient Local** → Stores messages so that even late subscribers can receive them.

### 3. **History** (How Many Messages to Keep?)
History controls how many messages are stored in memory.
- **Keep Last (N)** → Stores the last `N` messages (default: 1). Older messages are dropped when new ones arrive.
- **Keep All** → Stores all messages, as long as memory allows. Useful for debugging but can be **memory-intensive**.

### 4. **Liveliness** (Checking If Nodes Are Alive)
Liveliness ensures nodes are still active and responsive.
- **Automatic** → If the node is publishing messages, it's considered alive.
- **Manual** → the system will consider the publisher to be alive for another “lease duration” if it manually asserts that it is still alive (via a call to the publisher API)..
- Used in **critical control systems** where failure detection is necessary.

### 5. **Lease Duration**
The maximum period of time a publisher considered to be alive

### 6. **Deadline** (Max Allowed Time Between Messages)
- **Duration**-the expected maximum amount of time between subsequent messages being published to a topic.


### **Conclusion**
QoS in ROS 2 helps fine-tune communication to match system needs. Setting it up properly improves **efficiency, reliability, and real-time performance**. Picking the right QoS policy depends on system prioritizes.
