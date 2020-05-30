# ArcaNet Numbering System

## OSPF Area Numbering

Only 256 areas are to be used (0-255). Named with whole number, not IPv4
notation.

**Backbone area:** 0

IP addresses reserved for each area (N is area number):

 - 10.N.0.0/16
 - 127.(255-N).0.0/16 (loopback interfaces)

### OSPF Router IDs

Only 255 routers are allowed for each area (1-255). Router IDs should be
assigned as IPv4 addresses (including /24 subnets) on loopback interface
of the router.

Router ID should be in form 127.X.Y.1/32 where:

 - X = (255 - area number)
 - Y = (256 - router number within area)

Area Border Routers (ABRs) should have the area 0 router ID assigned (giving
them the highest router ID within sub-area).

## IPv4 Assignment and numbering

Each area administrator can provide their own numbering scheme.

### Area 0 allocation scheme

Each router within area is allocated /24 subnet in form 10.0.N.0/24 where N is
the router ID. Addresses from this allocation should be used for interfaces
within each router.

Area 0 MUST NOT contain any servers or any other device requiring IP address.

**EXCEPTION:** Managed switches SHOULD use addresses from 10.0.0.0/24 subnet,
as router local ID 0 is NOT ALLOWED.

Master router (router ID: 127.255.255.1) MUST claim address 10.0.0.1/24 and
provide DHCP service for non-router devices in area 0, if such are used.

### Sub-area recommendations

Subnets for each non-0 area are recommended to use the following addressing
scheme:

Assign 10.N.X.0/24 to VLAN X in area N.

## VLAN Numbering

To be determined
