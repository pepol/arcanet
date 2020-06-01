# ArcaNet Numbering System

## OSPF Area Numbering

Only 256 areas are to be used (0-255). Named with whole number, not IPv4
notation.

**Backbone area:** 0

IP addresses reserved for each area (N is area number):

 - 10.N.0.0/16
 - 127.(255-N).0.0/16 (loopback interfaces)

### OSPF Router IDs

Only 127 routers are allowed for each area (1-127). Router IDs should be
assigned as IPv4 addresses (including /24 subnets) on loopback interface
of the router.

Router ID should be in form 127.X.Y.1/32 where:

 - X = (255 - area number)
 - Y = (128 - router number within area)

Area Border Routers (ABRs) should have the area 0 router ID assigned (giving
them the highest router ID within sub-area).

## IPv4 Assignment and numbering

Each area administrator can provide their own numbering scheme.

### Area 0 allocation schema

Area 0 subnet is 10.0.0.0/16. This is divided into 2 subnets:

 - 10.0.0.0/17 - used for router connections
 - 10.0.128.0/17 - used for Anycast services and management addresses (e.g.
   for managed switches within area 0)

#### 10.0.0.0/17 - Router connection subnet

Each direct point-to-point connection between 2 routers is allocated a unique
/31 subnet.

Given 2 routers with IDs A and B, their subnet is: 10.0.A.(B\*2)/31

From this subnet, lower IP address should be assigned to router A and higher
to router B.

#### 10.0.128.0/17 - Anycast service and managed devices subnet

Area 0 MUST NOT contain any servers or any other device requiring IP address.

**EXCEPTION:** Managed switches SHOULD use addresses from 10.0.200.0/24 subnet

The subnets 10.0.128.0/24, 10.0.129.0/24, 10.0.130.0/24 are reserved for
Anycast service addresses.

### Anycast Service Assignments

#### DNS

To join anycast of our DNS services, select one of the following addresses to
announce anycast to:

 - 10.0.128.53/32 - a.name-servers.arca.
 - 10.0.129.53/32 - b.name-servers.arca.
 - 10.0.130.53/32 - c.name-servers.arca.

### Sub-area recommendations

Subnets for each non-0 area are recommended to use the following addressing
scheme:

Assign 10.N.X.0/24 to VLAN X in area N.

## VLAN Numbering

To be specified.
