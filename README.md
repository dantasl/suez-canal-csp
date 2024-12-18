# CSPm Specification

CSPm specification of processes to model the behavior on ships crossing the Suez Canal and the protocol they need to follow.

## The Suez Canal

The Suez Canal is a 193 km artificial waterway in Egypt that connects the Mediterranean Sea to the Red Sea, allowing ships to bypass the longer route around Africa. Unlike the Panama Canal, it has no locks, as both seas are at similar elevations. Ships travel in one direction at a time, organized into convoys, with designated waiting areas (bypasses) for alternating traffic. Priority rules may apply, with larger or high-priority vessels receiving precedence.

## Specification

The formal specification models the Suez Canal traffic system, as follows:

* Ships are grouped into convoys based on their direction (Northbound or Southbound).
* The canal operates in a single direction at a time, ensuring mutual exclusion.
* High-priority convoys are given precedence over low-priority ones when requesting passage.
* The system synchronizes convoys with a central controller that manages direction, convoy scheduling, and priority handling.

### Requirements

The specification requires that the system is compliant to the following:

* Only one direction (Northbound or Southbound) can use the canal at any given time.
* A convoy must traverse the canal as a group; no ship is left behind mid-passage.
* High-priority convoys must always be served before low-priority ones if both are waiting.
* The number of ships in a convoy does not exceed the canal's maximum allowed capacity.
* The convoy queue is processed in the order of priority, with ties broken by arrival order.

Additional liveness requirements include:

* Every high-priority convoy eventually traverses the canal.
* Low-priority convoys must not experience starvation (they eventually pass once no high-priority convoys are waiting).
* When one direction's traffic ends, the opposite direction must eventually be allowed to traverse.
* Once a convoy starts traversing the canal, all its ships complete the passage.
* Queue Clearing: All convoys waiting in the queue eventually traverse the canal.
