# Conflict Resolution

* Revision Based
* Time-Stamp Based  (Enterprise Edition only)

# XDCR 
For Documents greater than 256 bytes, XDCR fetched the target document metadata before replicating. Based on the conflict resolution of the target, the source will be either replicated or discarded. Once the replicated document reaches the target, similar comparison is done again.

For docuemnts less 256 bytes, the comparison is ignored for performance optimization.

## Revision Bases conflict resolution
Document's revision ID is used for resolution. Upon every update the revisiuon ID is incremented.

If both documents have same revision ID, then the following metadata are used for resilution,

* CAS value
* Expiration value (TTL)
* Document Flags 

## Timestamp based conflict resolution
Document timestamp stored in CAS is used to resolve conflicts. The document with recent timestamp prevails.
 
If both documents have same revision ID, then the following metadata are used for resilution,

* Revision ID
* Expiration value (TTL)
* Document Flags 

### Hybrid logical clock 
Combination of physical and logical clock to avoid issues raised when clocks of the nodes are not in sync.
**Physical clock** - Time returned by the system in milliseconds 
**Logical clock** - Counter that is increased when system clock yeilds a value less or equal to the current stored value

HLC(64 bit) = Physical clock(48 bit) + Logical counter(16 bit)