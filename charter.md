# Moderation Of unLinkable Endorsements (MOLE) Charter

The tools that websites have to help discriminate
between "good" and "bad" visitors
are quite limited.
The techniques sites have historically used to manage abuse
are increasingly ineffective against sophisticated adversaries.
At the same time, agentic and automated clients
are further complicating anti-abuse decision-making.

Though CAPTCHA is known to be ineffective and annoying for visitors,
it remains in wide use.
Websites are also turning to privacy-invasive methods,
like identification (email addresses, phone numbers)
or relying on client fingerprinting.

The most promising approaches for addressing this problem
use the existing relationships that people have with sites.
If other sites could draw on that information,
that would provide them with high confidence information about new visitors.

A simplistic implementation of cross-site information sharing
is incompatible with the privacy architecture of the web.
While cross-site cookies have been used in the past
as a basis for sharing information about visitors,
they are also abused for tracking and profiling.

Providing websites with actionable information
for managing abuse
requires cross-site signals
that are simultaneously high confidence and very low entropy.
At the same time, any system that is deployed to the web
needs to encourage open participation and resist centralization effects.

## Goals

The MOLE WG will develop an architecture and protocols
that support the distributed rate limiting of access to websites.
Rate limits will use a "capacity":
a small number of integer values
that are carried by clients between sites.
Sites can update the capacity held by clients
in response to observed activity
and make occasional queries
to confirm that the client holds a valid and acceptable capacity.

The MOLE WG will develop a mechanism for bootstrapping
the creation of client capacity
from a scarce, pre-existing "endorsement" from another site.

The MOLE WG will design privacy-preserving feedback mechanisms
to provide information to site operators
about the quality of the information they receive.

## Constraints

The MOLE WG will not develop new cryptographic primitives,
but instead adapt existing work to fit the target architecture.
Where possible, work from other groups, such as Privacy Pass,
will be adapted to fit the MOLE architecture,
rather than creating entirely new protocols.

The first products of the MOLE WG do not need to be safe from forgery
in the presence of a cryptographically-relevant quantum computer (CRQC).
All versions must maintain privacy and unlinkability
that resists a CRQC.

The MOLE WG will not constrain
how sites decide to create endorsements
or how they manage capacity.
The mechanisms it defines will only enable the transfer and management of that information.

## Coordination

The MOLE WG will coordinate closely with:

* the Privacy Pass working group,
  to ensure alignment of work and avoid duplication;

* the Crypto-Forum Research Group (CFRG) of the IRTF,
  who are actively documenting primitives that are relevant to the work in MOLE;

* the World Wide Web Consortium (W3C) or WHATWG,
  who might need to take on work to develop Web APIs
  to access MOLE capabilities in browsers;

* the HTTP working group (HTTPbis),
  for feedback on HTTP integration;

* the Privacy Preserving Measurement working group (PPM),
  if any feedback mechanisms could benefit from the product of that group; and

* the Web Bot Auth working group (WEBBOTAUTH),
  to share common aspects of designs and avoid duplication of effort.

## Deliverables

The MOLE WG will seek to deliver, to the IESG, documents on:

* MOLE system architecture, its components, and interactions between participants

* A protocol suite (one or more protocols) for the MOLE architecture
  that uses classical cryptographic techniques while being PQ-private

* A mapping of MOLE protocols to HTTP

* (Later) Protocol variants that are both PQ-private and PQ-unforgeable

* (Later) Protocols that provide feedback to key participants
  about operation of the protocol without compromising privacy goals
