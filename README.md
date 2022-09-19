# Summary
An API, common among vendors, is needed that supplies RFC8366 Ownership
Vounches used for RFC8572 sZTP.  It is necessary to automate the creation
and retrieval of OVs, because it is utterly impossible to manage them
manually.

It is not necessary that code is shared, but the same API is highly desirably.
We seek to define that API here.

This is a WiP.

# API Outline
An authenticated TLS connection is necessary.  Possibly OIDC or mTLS.

Devices must be identified by a serial number, manufacturer, and model
number.  The manufacturer is a tuple of a human-readable name and an
IANA Private Enterprise Number.  The model number must be the same
value used in the sZTP hw-model field of the bootstrap record and SNMP,
and represents the model of the TPM's parent - not the TPM itself.
Together these unambiguously identify a part.

Parts, whether by RMA or PO, must appear in the api well before they
arrive at their destination, so that they can immediately be placed in
service.

Parts are placed in a group.  A group is owned by user(s).  A user
may create (or delete) groups that become children of a group they own
and move parts from a group they own or any child group thereof to any
other such group.  The list of groups of which a user is a member, the
user members of a group, and the list of children of a group should be
retrievable.

An organization must be able to delegate parts to another organization
(or user), that might not be a subsidiary of the parent, to support
management separation by business unit, leasing agent, etc.  A delegate
might also have parts delegated to it directly from the vendor or other
organizations.  The part is not delegated, its group is.

An organization should be able to create (and delete) users to whom it can
delegate groups.

A list of parts by group must return the full device indentity tuple.
Retrieving an individual part, idenfitied by the tuple, must return its
EK (public key).

PDCs are assigned to a group.

OVs are retrieved for a specific device, with its group's PDC and a
lifetime.

# Protobuf definition
This is a WiP, but not ready for presentation.
