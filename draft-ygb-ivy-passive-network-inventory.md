---
coding: utf-8

title: A YANG Data Model for Passive Network Inventory

abbrev: Passive Network Inventory YANG Model
docname: draft-ygb-ivy-passive-network-inventory-01
workgroup: IVY Working Group
category: std
ipr: trust200902

stand_alone: yes
pi: [toc, sortrefs, symrefs, comments]

author:
  -
    name: Chaode Yu
    org: Huawei
    email: yuchaode@huawei.com
  -
    name: Aihua Guo
    org: Futurewei
    email: aihuaguo.ietf@gmail.com
  -
    name: Italo Busi
    org: Huawei
    email: italo.busi@huawei.com
  -
    name: Mohammad Boroon
    org: Highstreet
    email: mohammad.boroon@highstreet-technologies.com
  -
    name: Sergio Belotti
    org: Nokia
    email: sergio.belotti@nokia.com
  -
    name: Tom Van Caenegem
    org: Nokia
    email: tom.van_caenegem@nokia.com
  -
    name: Swaminathan 1. S.
    org: Nokia
    email: swaminathan.1.s@nokia.com
  -
    name: Swaminathan B.
    org: Nokia
    email: swaminathan.b@nokia.com
  -
    name: Nigel Davis
    org: Ciena
    email: ndavis@ciena.com
  -
    name: Mauro Tilocca
    org: FiberCop
    email: mauro.tilocca@fibercop.it
  -
    name: Brad Peters
    org: NBN
    email: bradpeters@nbnco.com.au
  -
    name: Bin Yu Yun
    org: ETRI
    email: byyun@etri.re.kr
  -
    name: Yucong Liu
    org: China Mobile
    email: liuyucongyjy@chinamobile.com
  -
    name: Yang Zhao
    org: China Mobile
    email: zhaoyangyjy@chinamobile.com
  -
    name: Avinash Sakalabhaktula
    org: Radisys
    email: Avinash.Sakalabhaktula@radisys.com




--- abstract

   This document presents a YANG data model for tracking and managing passive network
   inventory. The model enhances the base model outlined in {{!I-D.draft-ietf-ivy-network-inventory-yang}}
   and is intended for use in the northbound interface of a domain controller as defined in
   {{!RFC8453}}. 
 
--- middle

# Introduction

   Passive infrastructure refers to the underlying infrastructure of a telecommunication network that is 
   not actively detectable or managable. It typically includes non-powered, non-communicating devices and components,
   such as cabinets, cables, connectors, splitters, antennas, distribution frames, etc., that are either hosted 
   within an actively managed device or deployed along the physical pathway between active devices.
   Passive infrastructure serves as physical connections between active network devices, forming the 
   backbone for network topology. As a crucial part of communication networks,the inventory information
   for these devices is also essential for inventory management.
   
   {{!I-D.draft-ietf-ivy-network-inventory-yang}} incorporates the component concept from {{!RFC8348}} to detail the equipment and holder information of a NE. This encompasses chassis, slot/sub-slot, board/sub-board, port, and transceiver. As these items are recognized by the NE through internal protocols, the passive devices that cannot be discovered by the NE are thus not included in the modeling and needs to be addressed.

   {{!I-D.draft-ietf-ivy-network-inventory-location}} emphasizes the relative and geographic location, e.g. equipment room, geo-loation for NE. A passive device is deployed in a certain location visible by the operator, and thus can reference the location defined by {{!I-D.draft-ietf-ivy-network-inventory-location}}.
   
   This document focuses on modeling passive device inventory. The scope of this model is intended to be applicable to a varity types of networks, including but not limited to, IP/MPLS, optical access, optical transport and microwave networks.
   The methods for discovering these devices are implementation-specific and fall outside the scope of this document.
   
# Examples of Passive Network Inventory
   Network segments built on different technologies share many common passive infrastructure components across the system. To explore the practical applications of these components, we can examine example scenarios for optical access networks, optical transport systems, and microwave networks. 
   
## Passive Infrastructure in Optical Transport Networks
   Passive infrastructure in optical transport networks serves as the backbone for high-capacity data transmission. Key components include fiber optic cables, which act as the primary medium of long distance transmission. Optical connectors, patch panels, and splice enclosures are crucial for joining and managing fiber links. Couplers and splitters are used for signal distribution and combining. 
   
   Within a phyical network element (NE) there are also presence of passive components. For example, fiber optic cables are used to connect the ports of different modules within the same or between different chassises. Attenuators, on the other hand, are placed at places through connectors or built-in modules for reducing optical power.
   
   {{fig-example-optical-transport}} illustrates a typical passive infrastructure for a point-to-point optical transport network.   

~~~~ ascii-art
                                  Port
+--------------+                  +-+                 +--------------+
| +---+        |<--Cable--->+-----+ +----+<--Cable--->|        +---+ |
| |  +++       |            |     +-+    |            |       +++  | |
| |  ++* +---+ |Cable  Cable|    /   \   |Cable  Cable| +---+ *++  | |
| |NE |\+++  | |Seg. - Seg. |  /      \  |Seg. - Seg. | |  +++/| NE| |
| +---+ *++ +++|<-->| |<-->+++/        \+++<->| |<--->|+++ ++* +---+ |
|        |  + +|----| |----+ |----------| +---| |-----|+ +  |        |
|       +++ +++|----| |----+++\        /+++---| |-----|+++ +++       |
| +---+/*++  | |     -      |  \      /  |     -      | |  ++*\+---+ |
| |  +*+ |ODF| |    Joint   |   \    /   |    Joint   | |ODF| +*+  | |
| |  +++ +---+ |    Box     |    \  /    |    Box     | +---+ +++  | |
| |NE |        |            |     *-+    |            |        | NE| |
| +---+        |            +-----+ +----+            |        +---+ |
|Central Office|                  +-+                 |Central Office|
+--------------+              Fiber                   +--------------+
                              Distribution
                              Box
~~~~
{: #fig-example-optical-transport title="Passive Infrastructure for Optical Transport Networks"}

## Passive Infrastructure in Optical Access Networks
   Passive infrastructure in optical access networks, often referred to as Optical Distribution Network (ODN), is the physical fiber opticnetwork that connects the Optical Line Terminal (OLT) in the central office to the Optical Network Unit/Terminal (ONU/ONT) at the user's location. ODN uses one or multiple cascaded passive optical splitter to divide the signal from a single OLT into multiple paths to serve multiple users using a single fiber. ODN comprises optical fiber cables, connectors, and many auxiliary components. There are multiple types of fibers, including feeder fibers (connecting the OLT to a fiber distribution point (FDT)), distribution fibers (connecting the distribution point to access points), and drop fibers (connecting access points to ONUs/ONTs). The ODN cabinet acts as a central point where different fiber optic cables and components are hosted, and these ODN cabinets are often located on street corners, utility poles, or other accessible areas along the route to the end users.
   
   {{fig-example-optical-access}} illustrates a typical passive infrastructure for optical access networks.   

~~~~ ascii-art

                                                          Drop
                                                          Cable
                                                          <--->
                                                       +-+     +-+ONU
+--------------+                                       | |-----+-+
| +---+        |<-Feeder Cable->   <-Distr.->            |
| |  +++       |                     Cable    /|-------| |-----+-+ONU
| |  ++* +---+ | Cable    Cable              / |       +-+     +-+
| |NE |\+++  | | Seg.  -  Seg.    /|--------x  |FDT
| +---+ *++ +++|<---->/ \<---->  / |         \ |       +-+
| (OLT)  |  + +|------| |------x/  |          \|-------| |-----+-+ONU
|       +++ +++|------| |------x   | cccccccc          +-+     +-+
| +---+/*++  | |      \ /       \  | c   /| c         Fiber
| |  +*+ |ODF| |       -         \ | c  / | c         Access
| |  +++ +---+ |     Joint        \|-c-x  | c         Point
| |NE |        |     Box        FDT  c  \ | c                  +-+ONU
| +---+        |                     c   \|-c------------------+-+
| (OLT)        |                     c FDT <c---Drop Cable---->
|              |                     c      c
|Central Office|                     cccccccc
+--------------+                     Cabinet

~~~~
{: #fig-example-optical-access title="Passive Infrastructure for Optical Access Networks"}

## Passive Infrastructure in Microwave Networks
TBD

# Terminology and Notations

## Requirements Notations
{::boilerplate bcp14}

## Terminology
  The following terms are defined in {{!RFC7950}} and are not redefined here:

 - client
 - server
 - augment
 - data model
 - data node

  The following terms are defined in {{!RFC6241}} and are not redefined here:

 - configuration data
 - state data

 The following terms are defined and used in this document.
   
   - Passive device: refers to a physical device within a network that does not require external power to function, and simply manipulates signals through processes like transmission, reflection, splitting, filtering, or attenuation without actively amplifying or generating the signal. Examples include optical fibers, splitters, couplers, and optical filters, all of which are used to direct and manage light signals within a system without needing electricity. A passive device typically does not have management interfaces and is typically deployed in a location tracked by the network operator.
   - Active device: refers to a physical device that contains hardware and software and is managable through communication interfaces. Network elements defined by {{!I-D.draft-ietf-ivy-network-inventory-yang}} are examples of active device. 
   - Optical Cable: Refers to a wire that uses optical fiber as a medium to transmit optical signals. Optical cable is a concept of a collection, consisting of one or multiple optical cable segments connected by optical cable connectors. The equipment at both ends of the optical cable can be an optical distribution frame, an optical cross-connection box, or an optical splitter box.
   - Optical Cable Segment: refers to a section of optical cable where the number of fiber cores between two optical junctions remains unchanged. Optical cable segments can be spliced or fused through a joint box, connected through an optical distribution frame (ODF), or fiber jumpers. An optical fiber segment contains multiple fiber cores, or strands.

## Tree Diagram

   Tree diagrams used in this document follow the notation defined in
   {{!RFC8340}}.
   
## Prefixes in Data Node Names

   In this document, names of data nodes and other data model objects
   are prefixed using the standard prefix associated with the
   corresponding YANG imported modules, as shown in {{tab-prefixes}}.

   | Prefix   | YANG Module                  | Reference         |
   |----------|------------------------------|-------------------|
   | ni       | ietf-network-inventory       | RFC XXXX          |
   | nil      | ietf-ni-location             | RFC YYYY          |
{: #tab-prefixes title="Prefixes and Corresponding YANG Modules"}

RFC Editor Note:
Please replace XXXX with the RFC number assigned to {{!I-D.draft-ietf-ivy-network-inventory-yang}}.
Please replace YYYY with the RFC number assigned to {{!I-D.draft-ietf-ivy-network-inventory-location}}.
Please remove this note.

# Modeling Considerations

## Relationship with Network Inventory
TBD

## Relationship with Topology
TBD

# YANG Model Overview

   The YANG data model in this draft augments the model defined in {{!I-D.draft-ietf-ivy-network-inventory-yang}} with the following information:
   - Passive devices: a list of passive devices with extended attributed reported by the domain controller.
   - Optical cables: a list of optical cables with each containing a list of cable segments.
   
# Model Tree Diagram
~~~~
{::include ./ietf-ni-passive-device.tree}
~~~~
{: #fig-ni-passive-tree title="Tree diagram for passive network inventory"}
   
# YANG Modules

## YANG Data Model for Passive Device Inventory
~~~~
   <CODE BEGINS> file "ietf-ni-passive-device@2024-10-21.yang"
{::include ./ietf-ni-passive-device.yang}
   <CODE ENDS>
~~~~
{: #fig-ni-passive-yang title="YANG model for passive network inventory"}   

# Manageability Considerations

   TBD.

# Security Considerations

   The YANG module specified in this document defines a schema for data
   that is designed to be accessed via network management protocols such
   as NETCONF {{!RFC6241}} or RESTCONF {{!RFC8040}}.  The lowest NETCONF layer
   is the secure transport layer, and the mandatory-to-implement secure
   transport is Secure Shell (SSH) {{!RFC6242}}.  The lowest RESTCONF layer
   is HTTPS, and the mandatory-to-implement secure transport is TLS
   {{!RFC8446}}.

   The NETCONF access control model {{!RFC8341}} provides the means to
   restrict access for particular NETCONF or RESTCONF users to a
   preconfigured subset of all available NETCONF or RESTCONF protocol
   operations and content.

   There are a number of data nodes defined in this YANG module that are
   writable/creatable/deletable (i.e., config true, which is the
   default).  These data nodes may be considered sensitive or vulnerable
   in some network environments.  Write operations (e.g., edit-config)
   to these data nodes without proper protection can have a negative
   effect on network operations.  Considerations in Section 8 of
   {{!RFC8795}} are also applicable to their subtrees in the module defined
   in this document.

   Some of the readable data nodes in this YANG module may be considered
   sensitive or vulnerable in some network environments.  It is thus
   important to control read access (e.g., via get, get-config, or
   notification) to these data nodes.  Considerations in Section 8 of
   {{!RFC8795}} are also applicable to their subtrees in the module defined
   in this document.

# IANA Considerations

   It is proposed to IANA to assign new URIs from the "IETF XML
   Registry" {{!RFC3688}} as follows:

~~~~
   URI: urn:ietf:params:xml:ns:yang:ietf-ni-passive-device
   Registrant Contact: The IESG
   XML: N/A; the requested URI is an XML namespace.
~~~~

   This document registers the following YANG module in the YANG Module Names
   registry {{!RFC6020}}.

~~~~
   name: ietf-ni-passive-device
   namespace: urn:ietf:params:xml:ns:yang:ietf-ni-passive-device
   prefix: ni-passive
   reference: RFC XXXX
~~~~

--- back