---
title: "Agent-to-Agent Authentication and Authorization"
abbrev: "A2A-Auth"
category: info

docname: draft-agent2agent-kasselman_lombardo-agent2agent-auth-latest
submissiontype: IETF  # also: "independent", "editorial", "IAB", or "IRTF"
number:
date:
consensus: true
v: 3
# area: AREA
# workgroup: WG Working Group
keyword:
 - next generation
 - unicorn
 - sparkling distributed ledger
venue:
#  group: WG
#  type: Working Group
#  mail: WG@example.com
#  arch: https://example.com/WG
  github: "PieterKas/agent2agent-auth-framework"
  latest: "https://PieterKas.github.io/agent2agent-auth-framework/draft-agent2agent-kasselman_lombardo-agent2agent-auth.html"

author:
 -
    fullname: "PieterKas"
    organization: Your Organization Here
    email: "pieter@defakto.security"

 -
    fullname: Jean-François Lombardo
    nickname: Jeff
    organization: AWS
    country: Canada
    email: jeffsec@amazon.com
normative:
  WIMSE_ID
    title: WIMSE Identifier
    target: https://datatracker.ietf.org/doc/draft-ietf-wimse-identifier/
  
  SPIFFE:
    title: Secure Production Identity Framework for Everyone
    target: https://spiffe.io/docs/latest/spiffe-about/overview/
    author:
    - org: Cloud Native Computing Foundation

informative:

...

--- abstract

This document proposes a framework for secure agent-to-agent (A2A) interactions leveraging existing standards such as OAuth 2.0 and the Workload Identity Management and Secure Exchange (WIMSE) architecture. Rather than defining new protocols, this document explores how existing and widely deployed stnadards can be applied or extended to establish agent-to-agent authentication and authorization. By doing so, it aims to provide a framewrok within which to identify use of existing standards and identify gaps and guide future standardization efforts for secure agent-to-agent authentication and authorization.

--- middle

# Introduction

TODO Introduction


# Conventions and Definitions

{::boilerplate bcp14-tagged}

# Agents are workloads
An Agent is a workload that iteratively interacts with a Large Language Model (LLM) and a set of tools that expose interfaces to underlying services and resources until a terminating condition, determined either by the LLM or by the agent’s internal logic, is reached. It may receive input from a user, or act autonomusly. {{fig-agent-basic}} shows a conceptual model of the AI Agent as a workload.

{{fig-agent-basic}} illustrates the high-level interaction model between the User, the AI Agent, the Large Language Model (LLM), the Tools invoked by the Agent, and the underlying Services and Resources accessed through those Tools.

~~~ ascii-art
               +----------------+
               | Large Language |
               |   Model (LLM)  |
               +----------------+
                     ^   |
                 (2) |   | (3)
                     |   v
+--------+       +------------+       +--------+       +-----------+
|  User  |--(1)->| AI Agent   |--(4)->| Tools  |--(5)->| Services  |
|        |       | (workload) |       |        |       |   and     |
|        |--(8)->|            |<-(7)--|        |<-(6)--| Resources |
+--------+       +------------+       +--------+       +-----------+
~~~
{: #fig-agent-basic title="AI Agent as a Workload"}

1. Optional: The User provides an initial request or instruction to the AI Agent.
2. The AI Agent forwards the available context to the LLM. Context isimplementation and deployment specific and may include User input, system prompt, tool descriptions, tool outputs and other relevant information.
3. The LLM returns a response to the AI Agent identifying which tools it should invoke.
4. Based on the LLM’s output, the AI Agent invokes the relevant Tools.
5. The Tools interacts with the underlying Services and Resources required to fulfill the requested operation.
6. The underlying Services and Resources returns the information requested by the Tools.
7. The Tools returns the information collected from the Services and Resources to the AI Agent, which sends the information as additional context to the Large Langugage Model, repeating steps 2-7 until the exit condition is reached and the task is completed.
8. Optional: Once the exit condition is reached in step 7, the AI Agent may return a response to the User.

As shown in {{fig-agent-basic}}, the AI Agent is a workload that needs and identifier and credentials with which to authenticate itself to the Large Langugage Model and Tools. Once it has authenticated, the Large Langugage Model and Tools must determine if the AI Agent is authorized to access it. If the AI Agent is acting on-behalf-of a User, the User needs to deelegate access to the AI Agent, and the context of the User needs to be preserved to inform authorization decisions.

This document describes how AI Agents should leverage existing standards defined by SPIFFE {{!SPIFFE}}, WIMSE, OAuth and SSF.

# Agent Identity Management System
An Agent Identity Management System ensure that the right Agent has access to the right resources and tools at the right time for the right reason. It consists out of the following components:

* **Agent Identifiers:** Unique identifier assigned to every Agent.
* **Agent Credentials:** Cryptographic binding between the Agent Identifier and attributes of the Agent.
* **Agent Attestation:** Mechanisms for determining and assigning the identifier and issue credentials based on measurements of the Agent's environment.
* **Agent Credential Provisioning:** The mechanism for provisioning credentials to the agent at runtime.
* **Agent Authentication:** Protocols and mechanisms used by the Agent to authenticate itself to Large Langugage Models or Tools (resource or server) in the system.
* **Agent Authorization:** Protocols and systems used to determine if an Agent is allowed to access a Large Langugage Model or Tool (resource or server).
* **Agent Monitoring and Remediation:** Protocols and mechanisms to dynamically modify the authorization decisions based on observed behaviour and system state.
* **Agent Auhtentication and Authorization Policy:** The configuration and rules for each of the Agent Identity Management System.
* **Agent Compliance:** Measurement of the state and fucntioning of the system against the stated policies.

# Agent Identifier
Agents MUST be uniquely identified to enable authentication and authorization. The Secure Production Identity Framework for Everyone (SPIFFE) identifier format is widely deployed and operationally mature. The SPIFFE workload identity model defines a SPIFFE identifier (SPIFFE ID) as a URI of the form spiffe://<trust-domain>/<path> that uniquely identifies a workload within a trust domain {{!SPIFFE}}.

The Workload Identity in Multi-System Environments (WIMSE) working group builds on the experiences gained by the SPIFFE community and defines the WIMSE workload identifier {{WIMSE_ID}} as a URI that uniquely identifies a workload within a given trust domain.

Because SPIFFE IDs are URI-based workload identifiers and their structure aligns with the identifier model defined in the WIMSE identifier draft, all SPIFFE IDs can be treated as valid WIMSE identifiers.

All Agents MUST be assigned a WIMSE identifier, which MAY be a SPIFFE ID. 

# Agent Credentials
Agents MUST have credentials that provide a cryptographic binding to the agent identifier. These credentials are considered primary credentials that are provisioned at runtime. The cryptographic binding is essential for establishing trust since an identifier on its own is insufficient unless it is verifiably tied to a key or token controlled by the agent. WIMSE define a profile of X.509 certificates and Workload Identity Tokens (WITs), while SPIFFE defines SPIFFE Verified ID (SVID) profiles of JSON Web Token (JWT-SVID), X.509 certificates (X.509-SVID) and WIMSE Workload Identity Tokens (WIT-SVID). SPIFFE SVID credentials are compatible with WIMSE defined credentials. The choice of an appropriate format depends on the trust model and integration requirements.

Agent credentials MUST be ephemeral, include an explicit expiration time, and MAY carry additional attributes relevant to the agent (e.g., trust domain, attestation evidence, or workload metadata). 

In some cases, agents MAY need to have access to a secondary credential format to acces a proprietary or legacy system that is not compatible with the X.509, JWT or WIT it is provisioned with. In these cases an agent MAY exchange their primary credentials through a credential exchange mechanisms (e.g., OAuth 2.0 Token Exchange, Transaction Tokens, Workload Identity Federation). This allows an agent to obtain a credential targeted to a specific relying party by leveraging the primary credential in its possession. 

Note: Static API keys are an anti-pattern for agent identity. They lack cryptographic binding, cannot convey attestation or provenance, and are difficult to rotate or scope, making them unsuitable for secure Agent-to-Agent authentication or authorization.

# Agent Attestation
Key point - agent attestation is the equivalent of identiy proofing. there are numerous mechanisms through which this may be achieved, which are deployment and risk specific. Reference WIMSE and SPIFFE approaches here.

# Agent Credential Provisioning
Key point - credentials are dynamically provisioned at runtime, they are short lived to remove need for expiry management. Provisioning includes initial provisioning and rotation. Refer to SPIFFE and WIMSE. Maybe hint at using SCIM here?

# Agent Authentication
Key point - agents may authenticate in a number of ways based on credentials, supported protocols and environment. Distinguish between network and application layer. Refernece WIMSE.

## Network layer authentication
MTLS

## Application layer authentication
WPT, HTTP Sig.

# Agent Authorization
Key point - OAuth is broadly supported and provides a delegation model for users to clients (aka agents). Agents can obtain acess tokens directly (client credentials flow, using above authentication methods) or it can be delegated to them by a user (OAuth flows). Make point that the access token includes the client_id, which is the same as the Agent ID (ore related to it) and can be used for authroization decisions, along with other claims in an Access Token (reference JWT Access token spec). Make provision for opaque tokens as well. Discuss Downscoping of agent authorization using transaction tokens. Discuss cross-domain authorization (use cases) and how it may be achieved (identity chaining and cross-domain authorization). Discuss human in the loop authroization. Note concerns, refer to cross-device BCP as examples of consent phishing attacsk. Talk about CIBA as a protocol.

Picture -> Access Token -> Transaction Token -> Domain 1 -> Domain 2

## Same Domain Authorization

### Initial Authorization
User Delegated Authroization Initial authorization - user or agent gets access token.

### Donwscoped, Time Bount, Context Enriched Agent Authorization
Transaction Tokens

### Agent-to-Resource Authorization
Present token, peform additional authorization (RBAC etc?)
Direct or via tools
Resources, services.

Agent -> Tool -> Service -> Resource

### Human-in-the loop
Agent framework problem -> human in the loop - confirm something that it can already do - agent framework capability - confirmation. Risk management flow.
Human in the loop - request esalated privelages. Step-up authorization - refernece the draft (maybe)

MCP Elicitation to agent to perform some browser things - start authz code grant flow.
CIBA

## Cross Domain Agent-to-Agent Authorization
Identiyt chaining, ID-Jag.

# Agent Monitoring and Remediation
Key point - ongoing monitoring and remediation is needed. Use protocols like SSE, CAEP to respond to changes in authorization. Note the need for ongoing logging and audit trails. Talk about end-to-end audit and how this is enabled by having agent identifiers.

# Agent Auhtentication and Authorization Policy
Key point - configuration and parameters for all the above constitutes policy. Not stnadardises and not recommended for standrdisation? Perhaps somethign about document format?

# Agent Compliance
Key point - audit against Agent Identity Policy - not standrdised and not recommended to standardise.

# Security Considerations

TODO Security


# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
