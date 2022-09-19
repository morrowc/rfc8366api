# Summary
An API, common among vendors, is needed that supplies RFC8366 Ownership
Vounches used for RFC8572 sZTP.  It is necessary to automate the creation
and retrieval of OVs, because it is utterly impossible to manage them
manually.

It is not necessary code is shared, but the same API is highly desirably;
why make a chore worse by making yourself a snowflake.  We seek to define
that API here.

# API Outline
authenticated TLS connection is necessary.  Possibly OIDC or mTLS.

Devices must be identified by a serial number, manufacturer, and model
number.  The manufacturer is a tuple of a human-readable name and an
IANA Private Enterprise Number.  The model number must be the same
value used in the sZTP hw-model field of the bootstrap record and
represents the model of the TPM's parent - not the TPM itself.  Together
these unambiguously identify a part.

Parts belonging to an organization, whether by RMA or PO, must appear
in the api well before they arrive at their destination.

An organization must be able to delegate parts to another organization
(or user), that might not be a subsidiary of the parent, to support
management separation by business unit, leasing agent, etc.  A delegate
might also have parts delegated to it directly from the vewndor or other
organizations.

An organization should be able to create (and delete) users to whom it can
delegate parts.

An organization, or its delegates, should be able to create and organize
parts by group.

A list if parts by organization or delegate, or group, must return the
full device indentity tuple.  Retrieving an individual part, idenfitied
by the tuple, must return its EK (public key).

Storage of multiple PDCs by per-organization or delegate, must be possible.
A PDX is referenced in OV requests by a hash.

OVs are retrieved for a specific device, with a referenced PDC and a
lifetime.

# Protobuf definition
This is existing, but not ready for presentation.
