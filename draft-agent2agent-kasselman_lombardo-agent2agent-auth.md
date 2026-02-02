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
    fullname: Pieter Kasselman
    organization: DeFakto
    email: "pieter@defakto.security"

 -
    fullname: Jean-François Lombardo
    nickname: Jeff
    organization: AWS
    email: jeffsec@amazon.com

normative:
  RFC9334: # Remote ATtestation procedureS (RATS) Architecture
  WIMSE_ID:
    title: "WIMSE Identifier"
    target: https://datatracker.ietf.org/doc/draft-ietf-wimse-identifier/
  WIMSE_ARCH:
    title: "Workload Identity in a Multi System Environment (WIMSE) Architecture"
    target: https://datatracker.ietf.org/doc/draft-ietf-wimse-arch/
  WIMSE_WPT:
    title: "WIMSE Proof Token"
    target: https://datatracker.ietf.org/doc/draft-ietf-wimse-wpt/
  WIMSE_HTTPSIG:
    title: "WIMSE Workload-to-Workload Authentication with HTTP Signatures"
    target: https://datatracker.ietf.org/doc/draft-ietf-wimse-http-signature/
  WIMSE_CRED:
    title: "WIMSE Workload Credentials"
    target: https://datatracker.ietf.org/doc/draft-ietf-wimse-workload-creds/
  SPIFFE:
    title: "Secure Production Identity Framework for Everyone"
    target: https://spiffe.io/docs/latest/spiffe-about/overview/
  SPIFFE_ID:
    title: SPIFFE-ID
    target: https://github.com/spiffe/spiffe/blob/main/standards/SPIFFE-ID.md
  SPIFFE_X509:
    title: X509-SVID
    target: https://github.com/spiffe/spiffe/blob/main/standards/X509-SVID.md
  SPIFFE_JWT:
    title: JWT-SVID
    target: https://github.com/spiffe/spiffe/blob/main/standards/JWT-SVID.md
  SPIFFE_BUNDLE:
    title: SPIFFE Bundle
    target: https://github.com/spiffe/spiffe/blob/main/standards/SPIFFE_Trust_Domain_and_Bundle.md#4-spiffe-bundle-format
  SPIFFE_FEDERATION:
    title: SPIFFE Federation
    target: https://github.com/spiffe/spiffe/blob/main/standards/SPIFFE_Federation.md
  RFC9421:
    title: HTTP Message Signatures
    target: https://datatracker.ietf.org/doc/rfc9421
  RFC6749:
    title: The OAuth 2.0 Authorization Framework
    target: https://datatracker.ietf.org/doc/rfc6749
  RFC9449:
    title: OAuth 2.0 Demonstrating Proof of Possession (DPoP)
    target: https://datatracker.ietf.org/doc/rfc9449
  RFC9700:
    title: Best Current Practice for OAuth 2.0 Security
    target: https://datatracker.ietf.org/doc/rfc9700
  RFC9396:
    title: OAuth 2.0 Rich Authorization Requests
    target: https://datatracker.ietf.org/doc/rfc9396
  RFC9126:
    title: OAuth 2.0 Pushed Authorization Requests
    target: https://datatracker.ietf.org/doc/rfc9126
  RFC9068:
    title: JSON Web Token (JWT) Profile for OAuth 2.0 Access Tokens
    target: https://datatracker.ietf.org/doc/rfc9068
  RFC8725:
    title: JSON Web Token Best Current Practices
    target: https://datatracker.ietf.org/doc/rfc8725
  RFC6750:
    title: "The OAuth 2.0 Authorization Framework: Bearer Token Usage"
    target: https://datatracker.ietf.org/doc/rfc6750
  RFC7662:
    title: OAuth 2.0 Token Introspection
    target: https://datatracker.ietf.org/doc/rfc7662
  RFC9701:
    title: JWT Response for OAuth 2.0 Token Introspection
    target: https://datatracker.ietf.org/doc/rfc9701
  RFC8693:
    title: OAuth 2.0 Token Exchange
    target: https://datatracker.ietf.org/doc/rfc8693
  RFC9728:
    title: OAuth 2.0 Protected Resource Metadata
    target: https://datatracker.ietf.org/doc/rfc9728/
  RFC8628:
    title: OAuth 2.0 Device Authorization Grant
    target: https://www.rfc-editor.org/rfc/rfc8628.html
  OAuth.Private.JWT.Auth-RFC7523:
    title: JSON Web Token (JWT) Profile for OAuth 2.0 Client Authentication and Authorization Grants
    target: https://datatracker.ietf.org/doc/html/rfc7523
  OAuth.mTLS.Auth-RFC8705:
    title: OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens
    abstract: https://datatracker.ietf.org/doc/html/rfc8705
  OAuth.step-up.Auth-RFC9470:
    title: OAuth 2.0 Step Up Authentication Challenge Protocol
    abstract: https://www.rfc-editor.org/rfc/rfc9470.html
  OpenIDConnect.AuthZEN:
    title: Authorization API 1.0
    target: https://openid.net/specs/authorization-api-1_0.html
    author:
    - name: Omri Gazitt
      role: editor
      org: Asserto
    - name: David Brossard
      role: editor
      org: Axiomatics
    - name: Atul Tulshibagwale
      role: editor
      org: SGNL
    date: 2026
  OpenIDConnect.CIBA:
    title: OpenID Connect Client-Initiated Backchannel Authentication Flow - Core 1.0
    abstract: https://openid.net/specs/openid-client-initiated-backchannel-authentication-core-1_0.html
  OAuth.TRAT:
    title: Transaction Tokens
    target: https://datatracker.ietf.org/doc/draft-ietf-oauth-transaction-tokens/
  OAuth.SPIFFE.CLient.Auth:
    title: OAuth SPIFFE Client Authentication
    target: https://datatracker.ietf.org/doc/draft-ietf-oauth-spiffe-client-auth
  OAuth.CIMD:
    title: OAuth Client ID Metadata Document
    target: https://datatracker.ietf.org/doc/draft-ietf-oauth-client-id-metadata-document
  MCP:
    title: Model Context Protocol
    target: https://modelcontextprotocol.io/specification

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
                           ▲   |
                          (2) (3)
                           |   ▼
+--------------+       +------------+       +-----------+       +-----------+
|  User /      |──(1)─►|  AI Agent  |──(4)─►|  AI Tools |──(5)─►| Services  |
|      /       |       | (workload) |       |           |       |   and     |
|     / System |◄─(8)──|            |◄─(7)──|           |◄─(6)──| Resources |
+--------------+       +------------+       +-----------+       +-----------+
~~~
{: #fig-agent-basic title="AI Agent as a Workload"}

1. Optional: The Client provides an initial request or instruction to the AI Agent.
2. The AI Agent forwards the available context to the LLM. Context isimplementation and deployment specific and may include User input, system prompt, tool descriptions, tool outputs and other relevant information.
3. The LLM returns a response to the AI Agent identifying which tools it should invoke.
4. Based on the LLM’s output, the AI Agent invokes the relevant Tools.
5. The Tools interacts with the underlying Services and Resources required to fulfill the requested operation.
6. The underlying Services and Resources returns the information requested by the Tools.
7. The Tools returns the information collected from the Services and Resources to the AI Agent, which sends the information as additional context to the Large Langugage Model, repeating steps 2-7 until the exit condition is reached and the task is completed.
8. Optional: Once the exit condition is reached in step 7, the AI Agent may return a response to the User.

As shown in {{fig-agent-basic}}, the AI Agent is a workload that needs and identifier and credentials with which to authenticate itself to the Large Langugage Model and Tools. Once it has authenticated, the Large Langugage Model and Tools must determine if the AI Agent is authorized to access it. If the AI Agent is acting on-behalf-of a User, the User needs to deelegate access to the AI Agent, and the context of the User needs to be preserved to inform authorization decisions.

This document describes how AI Agents should leverage existing standards defined by SPIFFE {{SPIFFE}}, WIMSE, OAuth and SSF.

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

# Agent Identifier {#agent-identifier}
Agents MUST be uniquely identified to enable authentication and authorization. The Secure Production Identity Framework for Everyone (SPIFFE) identifier format is widely deployed and operationally mature. The SPIFFE workload identity model defines a SPIFFE identifier (SPIFFE ID) as a URI of the form `spiffe://<trust-domain>/<path>` that uniquely identifies a workload within a trust domain {{SPIFFE}}.

The Workload Identity in Multi-System Environments (WIMSE) working group builds on the experiences gained by the SPIFFE community and defines the WIMSE workload identifier {{WIMSE_ID}} as a URI that uniquely identifies a workload within a given trust domain.

Because SPIFFE IDs are URI-based workload identifiers and their structure aligns with the identifier model defined in the WIMSE identifier draft, all SPIFFE IDs can be treated as valid WIMSE identifiers.

All Agents MUST be assigned a WIMSE identifier, which MAY be a SPIFFE ID.

# Agent Credentials {#agent-credentials}
Agents MUST have credentials that provide a cryptographic binding to the agent identifier. These credentials are considered primary credentials that are provisioned at runtime. The cryptographic binding is essential for establishing trust since an identifier on its own is insufficient unless it is verifiably tied to a key or token controlled by the agent. WIMSE define a profile of X.509 certificates and Workload Identity Tokens (WITs) {{WIMSE_CRED}}, while SPIFFE defines SPIFFE Verified ID (SVID) profiles of JSON Web Token (JWT-SVID), X.509 certificates (X.509-SVID) and WIMSE Workload Identity Tokens (WIT-SVID). SPIFFE SVID credentials are compatible with WIMSE defined credentials. The choice of an appropriate format depends on the trust model and integration requirements.

Agent credentials MUST be ephemeral, include an explicit expiration time, and MAY carry additional attributes relevant to the agent (e.g., trust domain, attestation evidence, or workload metadata).

In some cases, agents MAY need to have access to a secondary credential format to acces a proprietary or legacy system that is not compatible with the X.509, JWT or WIT it is provisioned with. In these cases an agent MAY exchange their primary credentials through a credential exchange mechanisms (e.g., OAuth 2.0 Token Exchange, Transaction Tokens, Workload Identity Federation). This allows an agent to obtain a credential targeted to a specific relying party by leveraging the primary credential in its possession.

Note: Static API keys are an anti-pattern for agent identity. They lack cryptographic binding, cannot convey attestation or provenance, and are difficult to rotate or scope, making them unsuitable for secure Agent-to-Agent authentication or authorization.

# Agent Attestation
Agent attestation is the identity-proofing mechanism for AI agents. Just as humans rely on identity proofing during account creation or credential issuance, agents require a means to demonstrate what they are, how they were instantiated, and under what conditions they are operating. Attestation evidence feeds into the credential issuance process and determines whether a credential is issued, the type of credential issued and the contents of the credential.

Multiple attestation mechanisms exist, and the appropriate choice is deployment, and risk, specific. These mechanisms may include hardware-based attestations (e.g., TEE evidence), software integrity measurements, supply-chain provenance, platform and orchestration-layer attestations, or operator assertions. Depending on the risk involved, a single attestation may be sufficient, or, in higher risk scenarios, multi-attestation may be requred.

The Remote ATtestation Procedures (RATS) architecture (see {{RFC9334}}) provides a general model for producing, conveying, and verifying attestation evidence. RATS defines the roles of Attester, Verifier, and Relying Party, as well as the concept of Evidence, Endorsements, and Attestation Results.

Workload identity management systems can use different attestation mechanisms and implementations (including RATS), to represent attestation evidence and deliver it to credential provisioning systems.

# Agent Credential Provisioning
Agent credential provisioning refers to the runtime issuance, renewal, and rotation of the credentials an agent uses to authenticate and authorize itself to other agents. Agents may be provisioned with one or more credential types as described in {{agent-credentials}}. Unlike static secrets, agent credentials are provisioned dynamically and are intentionally short-lived, eliminating the operational burden of manual expiration management and reducing the impact of credential compromise. Agent credential provisioning must operate autonomously, scale to high-churn environments, and integrate closely with the attestation mechanisms that establish trust in the agent at each issuance or rotation event.

Agent credential provisioning typically includes two phases:

1. **Initial Provisioning**: The process by which an agent first acquires a credential bound to its identity. This often occurs immediately after deployment or instantiation and is based on verified properties of the agent (e.g., deployment context, attestation evidence, or orchestration metadata).
2. **Rotation/Renewal**: The automatic refresh of short-lived credentials before expiration. Continuous rotation ensures that credentials remain valid only for the minimum necessary time and that authorization state reflects current operational conditions.

The use of short-lived credentials provides a signiifcant improvement in the risk profile and risk of credential exposure. It provides an alternative to explicit revocation mechanisms and simplifies lifecycle management in large, automated environments.

Deployed frameworks such as {{SPIFFE}} provide concrete mechanisms for automated, short-lived credential provisioning at runtime based on workload attestation. In addition to issuing short-lived credentials, {{SPIFFE}} also provisions ephemeral cryptographic key material bound to each credential, further reducing the risks associated with compromising long-lived keys.

# Agent Authentication
Agents may authenticate to one another using a variety of mechanisms, depending on the credentials they possess, the protocols supported in the deployment environment, and the risk profile of the application. As described in the WIMSE Architecture {{WIMSE_ARCH}}, authentication can occur at either the network layer or the application layer, and many deployments rely on a combination of both.

## Network layer authentication
Network-layer authentication establishes trust during the establishment of a secure transport channel. The most common mechanism used by agents is mutual TLS (mTLS), in which both endpoints present X.509-based credentials and perform a bidirectional certificate exchange. When paired with short-lived workload identities—such as those issued by SPIFFE or WIMSE—mTLS provides strong channel binding and cryptographic proof of control over the agent’s credential.

mTLS is particularly well-suited for environments where transport-level protection, peer authentication, and ephemeral workload identity are jointly required. It also simplifies authorization decisions by enabling agents to associate application-layer requests with an authenticated transport identity.

**Limitations** There are scenarios where transport-layer authentication is not desirable or cannot be relied upon. In architectures involving intermediaries—such as API gateways, service meshes, load balancers, or protocol translators, TLS sessions are often terminated and re-established, breaking the end-to-end continuity of transport-layer identity. Similarly, some deployment models (e.g., serverless platforms, multi-tenant edge environments, or cross-domain topologies) may obscure or abstract transport identity, making it difficult for relying parties to bind application-layer actions to a transport-level credential. In these cases, application-layer authentication provides a more robust and portable mechanism for expressing agent identity and conveying attestation or policy-relevant attributes.

## Application layer authentication
Application-layer authentication allows agents to authenticate independently of the underlying transport. This enables end-to-end identity preservation even when requests traverse proxies, load balancers, or protocol translation layers.

The WIMSE working group defines the following authentication mechanisms that may be used by agents:

### WIMSE Proof Tokens (WPTs) {#wpt}
WIMSE Workload Proof Tokens (WPTs) are a protocol-independent, application-layer mechanism for proving possession of the private key associated with a Workload Identity Token (WIT). WPTs are generated by the agent, using the private key matching the public key in the WIT. A WPT is defined as a signed JSON Web Token (JWT) that binds an agent’s authentication to a specific message context, for example, an HTTP request, thereby providing proof of possession rather than relying on bearer semantics {{WIMSE_WPT}}.

WPTs are designed to work alongside WITs {{WIMSE_CRED}} and are typically short-lived to reduce the window for replay attacks.  They carry claims such as audience (aud), expiration (exp), a unique token identifier (jti), and a hash of the associated WIT (wth). A WPT may also include hashes of other related tokens (e.g., OAuth access tokens) to bind the authentication contexts to specific transaction or authorizations details.

Although the draft currently defines detailed usage for HTTP (via a Workload-Proof-Token header), the core format is protocol-agnostic, making it applicable to other protocols. Its JWT structure and claims model allow WPTs to be bound to different protocols and transports, including asynchronous or non-HTTP messaging systems such as Kafka and gRPC, or other future protocol bindings. This design enables relying parties to verify identity, key possession, and message binding at the application layer even in environments where transport-layer identity (e.g., mutual TLS) is insufficient or unavailable.

###  HTTP Message Signatures (HTTP Sig)
The WIMSE Workload-to-Workload Authentication with HTTP Signatures specification {{WIMSE_HTTPSIG}} defines an application-layer authentication profile built on the HTTP Message Signatures standard {{RFC9421}}. It is one of the mechanisms WIMSE defines for authenticating workloads in HTTP-based interactions where transport-layer protections may be insufficient or unavailable. The protocol combines a workload’s Workload Identity Token (WIT), which conveys attested identity and binds a public key, with HTTP Message Signatures using the corresponding private key, thereby providing proof of possession and message integrity for individual HTTP requests and responses. This approach ensures end-to-end authentication and integrity even when traffic traverses intermediaries such as TLS proxies or load balancers that break transport-layer identity continuity. The profile mandates signing of key request components (e.g., method, target, content digest, and the WIT itself) and supports optional response signing to ensure full protection of workload-to-workload exchanges.

# Agent Authorization
During agent execution, authorization must be enforced at all the components involved in the process to provide an in-depth protection of the resources that might be interacted with. For each component, we must consider the following 3 phases:
- Negotiation between the component and its caller on the required pieces of authorization required to interact with the component
- Acquisition of the piece of authorization by the caller at the authorization server authoritative for the component it wants to communication
- Validation of the piece of authorization in the context of the request by the component

Those phases rely on the following standards for enforcement of the access control:
- {{RFC6749}} is an established and maintained framework of specifications for requesting, acquiring, and proving ownership of pieces of authorization in the form of bearer tokens.
- {{OpenIDConnect.AuthZEN}} is a new specification for exchanging authorization requests and decisions between the layer acting at the Policy Enforcement Point (PEP) and a Policy Decision Point (PDP).
- {{OAuth.TRAT}} is new specification for formatting pieces of authorization in the form of transaction bound bearer tokens.

~~~ ascii-art
                       +----------------+
                       | Large Language |
                       |   Model (LLM)  |
                       +----------------+
                              ▲   |
                              │   |
                              |   ▼
+--------------+         +------------+         +-----------+         +-----------+
|  User /      |─(A)(C)─►|  AI Agent  |─(E)(H)─►| AI Tools  |─(J)(M)─►| Services  |
|      /       |         | (workload) |         |           |         |   and     |
|     / System |◄────────|            |◄────────|           |◄────────| Resources |
+--------------+         +------------+         +-----------+         +-----------+
     ▲                       ▲  ▲                   ▲   ▲                ▲
     |    ┌──(F)─────────────┘  |                   |   |                |
     |    |   ┌───(D)───────────┘                  (I)  |                |
     |    |   |  +---------------+                  |  (K)              (N)
    (B)   |   |  |    Policy     |                  |   |                |
     |    |   └─►|   Decision    |◄─────────────────┘   |                |
     |    |      |    Point      |◄─────────────────────┼────────────────┘
     |    |      +---------------+                      |
     |    |             ▲                               |
     |    |          (G)(L)                             |
     |    |             ▼                               |
     |    |      +---------------+                      |
     |    └─────►| Authorization |◄─────────────────────┘
     └──────────►|   server      |
                 +---------------+
~~~


> Key point - OAuth is broadly supported and provides a delegation model for users to clients (aka agents). Agents can obtain access tokens directly (client credentials flow, using above authentication methods) or it can be delegated to them by a user (OAuth flows). Make point that the access token includes the client_id, which is the same as the Agent ID (ore related to it) and can be used for authorization decisions, along with other claims in an Access Token (reference JWT Access token spec). Make provision for opaque tokens as well. Discuss Downscoping of agent authorization using transaction tokens. Discuss cross-domain authorization (use cases) and how it may be achieved (identity chaining and cross-domain authorization). Discuss human in the loop authorization. Note concerns, refer to cross-device BCP as examples of consent phishing attacks. Talk about CIBA as a protocol.

## System to AI Agent
### (A) Negotiation - OPTIONAL

#### Flow

Following {{RFC9728}}, the System MUST act as an OAuth2 client. It MUST interact with the AI Agent on its metadata endpoint which MUST be an OAuth 2.0 protected resource as defined by {{RFC9728}}.

The System will then understand which Authorization Server MUST be the authority this AI Agent; which scopes or authorization details values MAY be required to access this AI Agent; and if extension mechanisms MAY be required to fulfil.

#### Security

The System MUST follow the best current practices described in {{RFC9700}}.

### (B) Initial Authorization

Based on the information collected as part of (A) or based on its configuration, the System MUST initiate an authorization request to the Authorization Server acting as authority for the AI Agent.

#### Flow

For this, the System MUST use one of the grant types described in {{RFC6749}} as follows:

- In a case of the System is acting on its behalf, it MUST start a client credential grant flow as described in section 1.3.4 of {{RFC6749}};
- In the case of the System is acting on behalf of a user:
  - If the System can interact directly with the user (e.g., browser-based), the System MUST use the authorization code grant flow as described in Section 4.1 of {{RFC6749}};
  - If the System has limited input capabilities, but the User is present at the device, the System MUST use the Device Authorization Grant {{RFC8628}};
  - If the User is not present at the consuming device (decoupled flow), the System MUST use Client-Initiated Backchannel Authentication {{OpenIDConnect.CIBA}}.

#### Extensions

As part of the grant flow, the User / System MUST also fulfill all the expected extensions it has an understanding of. For example, not exhaustively:
- Binding the requested tokens to a possessed key as defined in {{RFC9449}} or {#wpt}
- Requesting additional authorization details as defined in {{RFC9396}} or {{RFC9126}}

#### Identification

The System MUST act as an OAuth2 Client which MAY be assigned a WIMSE identifier, which MAY be a SPIFFE ID.

If so, the System MUST provide a way to resolve one value to the other, either through:
- A metadata document URL used OAuth2 Client identifier as defined in {{OAuth.CIMD}};
- Metadata information provided as part of the Private Key JWT OAuth client credential as defined in {{OAuth.Private.JWT.Auth-RFC7523}}
- Public Certificate information provided as part of the mutual TLS OAuth client credential as defined in {{OAuth.mTLS.Auth-RFC8705}}

#### Authentication

The System MUST authentication using either:
- Private Key JWT OAuth client authentication as defined in {{OAuth.Private.JWT.Auth-RFC7523}}
- Mutual TLS OAuth client authentication as defined in {{OAuth.mTLS.Auth-RFC8705}}

#### Security

The System MUST follow the best current practices described in {{RFC9700}} for the interactions with the AI Agent and {{RFC8725}} when handling JWTs.

### (C) Access to the AI Agent

#### Flow

To access an AI Agent, the System MUST present its authorization credential as defined in section 7 of {{RFC6749}} as well as defined in {{RFC6750}}. The client MUST be able to process error codes as defined in section 3 of {{RFC6750}}.

The AI Agent MAY request additional details to be provided through a new authorization credentials using {{OAuth.step-up.Auth-RFC9470}} or error codes as defined in {{RFC6750}}.

#### Security

The client MUST follow the best current practices described in {{RFC9700}}.

### (D) Controlling access to the AI Agent

#### Flow

The AI Agent MUST validate the presented token as described in {{RFC6749}} as well as defined in {{RFC6750}}.

If token introspection is required, the AI Agent MUST follow {{RFC7662}} as well as {{RFC9701}}.

If the provided token is a JWT profiled token as defined in {{RFC9068}}, the AI Agent MUST follow the section 2 of this specification as part of the token validation.

If the AI Agent delegates its access control logic to a Policy decision point, it MUST follow {{OpenIDConnect.AuthZEN}} specification for requesting and receiving a decision for the access.

#### Security

TODO

## AI Agent to AI tools

> Interactions between an AI Agent and AI Tools are globally specified by {{MCP}}. Those sections explain the core specification, {{MCP}} is based on as well as the complementary specifications RECOMMENDED.

### (E) Negotiation

Following {{RFC9728}}, the AI Agent MUST interact with AI Tools on the metadata endpoint of an OAuth 2.0 protected resource to understand which Authorization Server is the authority this resource; which scopes or authorization details values MAY be required to access this resources; and if proof of possession needs to be presented as standardized with {{RFC9449}}.

### (F) AI Agent Authorization

Based on the information collected as part of (E), the AI Agent is initiating an authorization request with the Authorization Server acting as authority for the AI Tools.

Such authorization request can allow to down, change or translate scope; enrich the authorization with new details based on the context; extend the time boundaries of the authorization; or change from a delegation mode to an impersonation mode and reversely.

- If the AI Agent acts on its behalf as a system:
  - If it does not want or need to refer to the previous context, it MUST start a client credential grant flow as described in section 1.3.4 of {{RFC6749}};
  - If it does want or need to refer to the previous context, it MUST start a token exchange flow as described in {{RFC8693}}. The AI Agent will be able to decide in between obtaining tokens representing a Delegation or an Impersonation as described in section 1.1 of the specification.
- If the AI Agent acts on delegation by a user:
  - If the AI Agent can interact and want to interact with the user through the client, it MUST start an authorization code grant flow as described in section 1.3.1 of {{RFC6749}};
  - If the AI Agent cannot or does not want to interact with the user through the client, it MAY:
    - Start a token exchange flow as described in {{RFC8693}}. The AI Agent will be able to decide in between obtaining tokens representing a Delegation or an Impersonation as described in section 1.1 of the specification.
    - Start a client initated backchannel authorized request as described in {{OpenIDConnect.CIBA}}

> Transaction Tokens

## Agent-to-Resource Authorization
Present token, peform additional authorization (RBAC etc?)
Direct or via tools
Resources, services.

Agent -> Tool -> Service -> Resource

### Human-in-the loop
Agent framework problem -> human in the loop - confirm something that it can already do - agent framework capability - confirmation. Risk management flow.
Human in the loop - request esalated privelages. Step-up authorization - refernece the draft (maybe)

MCP Elicitation to agent to perform some browser things - start authz code grant flow.
CIBA

## Case of Multi-Domain Authorization

### Cross Domain Agent-to-Agent Authorization
Identiyt chaining, ID-Jag.


## Agent to Agent Authorization

# Agent Monitoring and Remediation - Jeff
Key point - ongoing monitoring and remediation is needed. Use protocols like SSE, CAEP to respond to changes in authorization. Note the need for ongoing logging and audit trails. Talk about end-to-end audit and how this is enabled by having agent identifiers.

# Agent Auhtentication and Authorization Policy - Discuss
Key point - configuration and parameters for all the above constitutes policy. Not stnadardises and not recommended for standrdisation? Perhaps somethign about document format?

# Agent Compliance - Discuss
Key point - audit against Agent Identity Policy - not standrdised and not recommended to standardise. Governance and observability. Perhaps we discuss and describe, but don't suggest standards here.

# Security Considerations

TODO Security


# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
