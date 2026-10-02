[STATUS: DRAFT]

# Name: Moderation Of unLinkable Endorsements (MOLE)

## Description

Web sites have always had to deal with the difficult question
of whether to provide service to newly arrived visitors.
By its nature, a new visitor on the web carries very little previous reputation
that a site might use to inform this choice.
This might be a new long-term customer.
Or, it could be a bot that wastes resources,
mounts credential stuffing attacks, commits ad fraud,
or otherwise engages in unwelcome behavior.

The trend has always been toward this decision being progressively harder.
Even though providing a site can be cheap,
any improvements in serving efficiency correlate with increasing scale
of both wanted and unwanted traffic.
At the same time,
the mechanisms that sites use to separate out unwanted bots are less effective.
CAPTCHA was always user hostile,
but it is now cheap for bots to solve,
with far better success rates than human users.
Fingerprinting can be helpful,
but it is mostly only good for insulating unrelated users from the worst effects of attack remediation.

In a setting where most trust indicators are negative,
a positive trust signal could be highly valuable to sites.
Privacy Pass was set up to address this need,
but experience with web deployments of the technology has demonstrated that
the Privacy Pass architecture is unsuited to delivering a solution that works for the web.
The web is a difficult environment to deploy to,
with strong privacy and anti-centralization goals that are very hard to meet.

MOLE sets out to develop an architecture with two parts.

The first piece is a system for supplying clients
with authenticated, and unlinkable state
that minimally provides some means of dynamic rate limiting use
across different web contexts (that is, websites).
Dynamic rate limiting means that websites can adjust a client's access
over time in response to its behavior,
rewarding good behavior and punishing abuse.
Though sites can update this state freely,
clients are able to limit how often a site can test
that the state meets its qualification criteria,
which is what reveals private information.
Testing a token can result in as small an information release as one bit per site.

The second part of the system supplements the first
by providing an anchoring endorsement token
that prevents clients from resetting their state constantly.
One of a set of entities issue a scarce endorsement token
that is used to bootstrap the first process.
Endorsement tokens need to be scarce
so they likely need to tie to something concrete,
like a digital identity, a payment, or user account.
These can come from diverse sources,
limiting centralization effects that come from systems of this form.
Importantly, redemption of endorsement tokens will not reveal the identity
of the entity that issued it,
only that it belongs to one of a set of entities trusted by the website.
This mitigates privacy and centralization risks,
whilst ensuring that the signal remains useful to sites.

These mechanisms have a number of potential uses beyond these goals.
Any working group would focus on the web anti-abuse scenario only.
The group would need to recharter to take on new use cases.
We expect other working groups to build on the work that is done here.
For example, WEBBOTAUTH is looking at using the output of MoLE
to enable the anonymous authentication of agents (draft-rescorla-anonymous-webbotauth).

The BoF session will look at the single use case of providing a signal to websites,
touch briefly on a few related use cases,
establish the viability of the mechanisms,
and discuss the charter for a working group.

## Required Details

- Status: WG forming
- Responsible AD: Deb Cooley (SEC)
- BOF proponents: Martin Thomson <mt@lowentropy.net>, David Schinazi <dschinazi.ietf@gmail.com>
- Number of people expected to attend: 150
- Length of session (1 or usually 2 hours): 2 hours
- Conflicts (whole Areas and/or WGs)
   - Chair Conflicts: n/a
   - Technology Overlap: privacypass, cfrg, webbotauth
   - Key Participant Conflict: Dennis Jackson, Watson Ladd, Chris Patton, Thibault Meunier, Sam Schlesinger

## Information for IAB/IESG

To allow evaluation of your proposal, please include the following items:

### Any protocols or practices that already exist in this space

Privacy Pass is clearly the most relevant work in this area.
Privacy Pass was initially chartered with the goal of developing
a privacy preserving rate limiting solution that could be deployed on the web.
Although Privacy Pass has delivered widely deployed solutions in other contexts,
efforts to deploy it on the open web have stalled with no standardized solution available.
The concerns that led to this outcome include
issuer centralization, effectiveness and privacy,
which were foreseen at the time the WG was chartered,
but have proved intractable in the 6 years since inception.

MOLE is based on learnings from Privacy Pass.
Those learnings show that addressing the web anti-abuse case
requires significant architectural and protocol changes
backed by a new cryptographic designs.

MOLE introduces a number of new protocol flows,
participant roles,
and concepts which would lead to considerable confusion
if cast in terms of the Privacy Pass architecture.
MOLE’s proposed architecture is provided as a resource below.

Besides the technical and architectural differences,
there are process reasons to favour a WG-forming BoF over trying to recharter Privacy Pass:

* PrivacyPass has suffered from low participation for several years,
  a BoF will attract the needed community input and consensus which a recharter would not.

* A BoF is the appropriate mechanism for ensuring the problem is well understood,
  tractable and deciding if the problem statement justifies additional work.

* A BoF is the appropriate mechanism for validating that the community is interested
  and there is sufficient support from implementers.

CFRG is currently looking at the building blocks for zero-knowledge protocols,
which would be central to the technical designs envisaged for MOLE.
This includes basic Sigma protocol building blocks (draft-irtf-cfrg-sigma-protocols)
and the Fiat-Shamir heuristic (draft-irtf-cfrg-fiat-shamir).
Both drafts formalize well understood and widely used constructions,
which MOLE would use.
The primary risk is that the CFRG effort is stalled or delayed,
in which caes the working group would either
seek to document designs without a dependency (on the basis that this is only engineering)
or to reference work developed by another entity
(C2SP has been identified as a potential candidate; https://c2sp.org).

### Which (if any) modifications to existing protocols or practices are required

* This working group will liaise with W3C groups
  who will define interfaces to the mechanisms designed here.

* The current set of drafts includes HTTP extensions (header fields, primarily)
  that can be used to carry the protocol alongside HTTP interactions.
  This is presently only a rough sketch,
  but as the core mechanisms mature,
  this work will seek to work out how to integrate with
  the work that Privacy Pass has already done in this area
  as well as the HTTP working group.

### Which (if any) entirely new protocols or practices are required

* The primary deliverable of any working group will be a suite of protocols
  that are suitable for deployment to the web.
  These might be executed in HTTP headers (as above)
  or using web (JavaScript) API interactions.

  * Note that the (existing) WEBBOTAUTH working group
    has decided to develop an anonymous,
    class-revealing authentication method for bots.
    The most promising proposal for that (draft-rescorla-anonymous-webbotauth)
    depends on some or maybe all the work that is being proposed in MOLE.

* MOLE will target cryptography which provides post-quantum unlinkability in all its work.
  This ensures that, if a cryptographically-relevant quantum computer (CRQC) is developed
  in the future,
  user privacy will not be impacted through harvest-now link-later attacks.
  However, MOLE could build initial designs on classical (EC) cryptography
  that does not provide post-quantum forgery resistance.
  Forgery-resistance is less pressing because the future CRQC developments
  will not impact the forgery-resistance of past deployments.

### Open source projects (if any) implementing this work

* The project (links below) includes implementation efforts
  for the core protocol pieces that MOLE will define.
  It is expected that these will be used by many deployments.
  Individuals from server-side participants in MoLE
  will also be present to discuss their intended use cases.

* All modern web browser engines are open source.
  The expectation is that this will be implemented across major browsers.
  Browser-developers from multiple engines will be present for discussions
  and will discuss their plans and progress.

* Contemporary solutions for agentic web access
  also use the same web browser engines as humans.
  Consequently the client implementations can be shared between both populations.

## Agenda

- Introduction
- Problem statement
- Architecture and feasibility
- High-level scope and discussion
- Charter

## Links to the mailing list, draft charter if any (for WG-forming BoF), relevant Internet-Drafts, etc.

- Mailing List: https://www.ietf.org/mailman/listinfo/mole
- This request: https://github.com/FIXME
- Draft charter: https://github.com/FIXME
- Relevant Internet-Drafts:
   - All: https://moderation-of-unlinkable-endorsements.github.io/internet-drafts/
   - Architecture: https://moderation-of-unlinkable-endorsements.github.io/internet-drafts/draft-jms-mole-architecture.html
- Project: https://github.com/Moderation-of-unLinkable-Endorsements/
