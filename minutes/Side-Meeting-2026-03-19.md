# Passive Inventory side meeting (March 19,2026)

## Participants

- Aihua Guo
- Bo Wu
- Brad Peters
- Ian Farrer
- Italo Busi
- Olga Havel
- Roberto Manzotti

## Agenda

Some clarification: passive components can be also part of an active NE. The term "passive device" is mainly referring to a group of passive components. An active NE (as currently modelled in the base inventory model) can contain both active and passive components.

Reviewed slide from Aihua (cable segmented into multiple segment):

- link to the slides: https://github.com/aguoietf/draft-ygb-ivy-passive-network-inventory/blob/main/materials/draft-ygb-ivy-passive-network-inventory-00-ietf-122%20-%20v1.pptx

Clarified that today the cable segments are modelled as child cables under the cable

The joint boxes (see Figure 1 and Figure 2 of the I-D) are modelled as passive devices and the A-end/Z-end represents where the child cables are connected to the joint boxes

It is needed to report the joint boxes within the passive inventory e.g., for reporting their geolocation

The patch panel can be modelled as a passive device where fibers from different cables are spliced

There was some discussion about the "fiber closures" which can contain multiple cables. Examples are available at the following URLs:

https://raycom.cz/templates/it-technologie/images/eye_products/87/pdf/cz/datasheet-and-ordering-guide-tenio-fiber-closures.pdf

https://www.commscope.com/product-type/hubs-closures-terminals-boxes/splice-closures/fiber-splice-closures/tenio/

https://www.alcadon.com/PDF/PDF2019/CW6618-000_Product_specifications.pdf

The "fiber closures" can be modelled as passive component within an active NE or passive device. The A-end/Z-end of the cables contained within the "fiber closures" are port components which do not belong to this component.

Another use case to consider is the modelling of the MPO/MPT cable:

https://majorcustomcable.com/product/cables/fiber-connectivity/mtp-mpo-cables/

This can be modelled as a multipoint cable with one A-end and multiple Z-ends. The numbering of the fibers within the cable need to be consistent in the A-end and Z-ends.

A different scenario is where there is a splitter along the fiber:

https://ecatalog.corning.com/optical-communications/AU/en/Fiber-Optic-Hardware/Terminals/OptiSheath%C2%AE-MultiPort-Splitter-Stubless-Terminal/p/optisheath-multiport-splitter-stubless-terminal

https://ecatalog.corning.com/optical-communications/AU/en/Fiber-Optic-Hardware/Terminals/OptiSheath%C2%AE-MultiPort-Splitter-Stubless-Terminal/p/optisheath-multiport-splitter-stubless-terminal

https://www.alldataresource.com/CommScope-CC8312-000-OCC1P-Wideband-Splitter-planar-singlemode-1-x-32-symmetrical-split-ratio-0-250-mm-cable-field-installable_p_601802.html

https://www.commscope.com/product-type/hubs-closures-terminals-boxes/access-terminals/fiber-terminals-hardened/itemmst-0nrh00-a0500u/

https://ecatalog.corning.com/optical-communications/AU/en/Fiber-Optic-Hardware/Terminals/OptiSheath%C2%AE-MultiPort-Flex-Splitter-Terminal/p/optisheath-multiport-flex-splitter-terminal

Roberto has shown an example of a component which can be either passive or active depending on how it is configured:

- [ ] @Roberto: please add a link

This can be easily modelled as a component within a NE if the passive devices are modelled as NEs and passive component as components within the NE.

The passive inventory model is still missing the description of how the fibers are spliced within passive devices which splice the fibers.

Open questions for further discussions/considerations:

1) Should we model passive devices as NEs?

2) If so, should we model any passive device as NEs (including cable joint boxes) or only some passive devices and have an ad-hoc model for cable joint boxes?

Note that a joint box can be modelled as a passive device/component which splice the cable (i.e., all the fibers within the cable as a group)

3) If all the passive devices are associated with a node in the physical topology, it is possible to have a direct navigation between the link and the cable and remove the A-end/Z-end from the cable (since this association can be inferred from the TPs terminating the link and the ports associated with these TPs). Would this modelling approach be beneficial (e.g., for SIMAP)?
