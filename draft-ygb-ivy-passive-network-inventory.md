---
coding: utf-8

title: A YANG Data Model for Passive Network Inventory

abbrev: Passive Network Inventory YANG Model
docname: draft-ygb-ivy-passive-network-inventory-00
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

--- abstract

   This document presents a YANG data model for passive device inventory information.
   The model enhances the base model outlined in {{!I-D.draft-ietf-ivy-network-inventory-yang}}
   and is intended for use in the northbound interface of a domain controller as defined in
   {{!RFC8453}}.
 
--- middle

# Introduction

   Passive devices typically include fiber, cable, optical splitters, and some passive sites. As a crucial part of communication networks, the inventory information for these devices is also essentialfor inventory management.
   
   {{!I-D.draft-ietf-ivy-network-inventory-yang}} incorporates the component concept from {{!RFC8348}} to detail the equipment and holder information of a NE. This encompasses chassis, slot/sub-slot, board/sub-board, port, and transceiver. As these items are recognized by the NE through internal protocols, the passive devices that cannot be discovered by the NE are thus not included in the modeling and needs to be addressed.

   {{!I-D.draft-ietf-ivy-network-inventory-location}} emphasizes the relative and geographic location, e.g. equipment room, geo-loation for NE. A passive device is deployed in a certain location visible by the operator, and thus can reference the location defined by {{!I-D.draft-ietf-ivy-network-inventory-location}}.
   
   This document focuses on modeling passive device inventory. The methods for discovering these devices 
   are implementation-specific and fall outside the scope of this document.

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
{: #fig-ietf-ns-topo-yang title="YANG model for passive network inventory"}   

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