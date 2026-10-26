# Moderation of unLinkable Endorsements (MOLE) Charter

The tools that websites have to help discriminate between “good” visitors
and bad ones are quite limited.
In the past, this means that sites resort to using a range of techniques
to defend themselves against abusive clients.
These techniques have proven to be increasingly less ineffective,
while being annoying and privacy-invasive.
For example, CAPTCHA is widely recognized as being ineffectual,
as automated solvers now trivially pass tests that many humans struggle with.
Websites are increasingly moving to more invasive methods,
such as asking for identification (email addresses, phone numbers)
or relying on client fingerprinting in order to curtail abuse.
In addition to this, agentic and automated clients
are creating new interaction models
that create complex demands on anti-abuse decision-making.

The most promising approaches for addressing this problem
use the reputation that people build up with sites
they have deeper or longer-lasting relationships with.
If other sites could draw on that information,
that would provide them with high confidence information about new visitors.

Unfortunately, a simplistic implementation of cross-site reputation
is incompatible with the privacy architecture of the web.
For instance, third-party cookies have been used in the past
as a basis for sharing reputation information.
However, most browsers actively seek to block cross-site cookies
because they are routinely abused for tracking and profiling.

Deployment to the web requires a system that can provide high confidence signals
with very low entropy.
At the same time, any system that is deployed to the web
needs to encourage open participation and resist centralization effects.

## Goals

The MOLE WG will develop an architecture and protocols
that support the sharing and management of site visitor reputation.
This includes a collection of low entropy signals
regarding visitor behavior that can change over time,
suitable for the deployment to the web.
Reputation will take the form of restricted state information
(a small number of integer values)
that can be separately updated and queried.

In addition to protocols for bootstrapping and managing reputation,
the MOLE WG will design and incorporate feedback mechanisms.
Feedback will provide actionable information about the quality of signals
that sites receive to the operators of the services that provide those signals.

The group will not develop new cryptographic primitives,
but instead adapt existing work to fit the target architecture.
Where possible, existing work in other groups, such as Privacy Pass,
will be adapted to fit the MoLE architecture,
rather than creating entirely new protocols.

Early versions of this do not need to be safe from forgery
in the presence of a cryptographically-relevant quantum computer (CRQC).
All versions must maintain privacy and unlinkability
that resists a CRQC.

Moreover, the MoLE WG will not specify mechanisms by which trust and reputation
are established for site visitors.
The mechanisms it defines will only enable the transfer and management of that information.

## Coordination

The MoLE WG will coordinate closely with:

* the Privacy Pass working group, to ensure alignment of work and avoid duplication;

* the Crypto-Forum Research Group (CFRG) of the IRTF,
  who are actively documenting primitives that are relevant to the work in MoLE;

* the World Wide Web Consortium (W3C) or WHATWG,
  who might need to take on work to develop Web APIs
  to access MoLE capabilities in browsers;

* the HTTP working group (HTTPbis),
  in the event that an HTTP-based protocol is developed;

* the Privacy Preserving Measurement working group (PPM),
  if any feedback mechanisms could benefit from the product of that group; and

* the Web Bot Auth working group (WEBBOTAUTH),
  to share common aspects of designs and avoid duplication of effort.

## Deliverables

The MoLE WG will seek to deliver, to the IESG, documents on:

* MoLE system architecture, its components, and interactions between participants

* A protocol suite (one or more protocols) for the MoLE architecture
  that uses classical cryptographic techniques while being PQ-private

* A mapping of MoLE protocols to HTTP

* (Later) Protocol variants that are both PQ-private and PQ-unforgeable

* (Later) Protocols that provide feedback to key participants
  about operation of the protocol without compromising privacy goals
