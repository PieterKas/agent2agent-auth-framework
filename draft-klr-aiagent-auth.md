---
title: "AI Agent Authentication and Authorization"
abbrev: "AI-Auth"
category: info

docname: draft-klr-aiagent-auth-latest
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
  latest: "https://PieterKas.github.io/agent2agent-auth-framework/draft-klr-aiagent-auth.html"

author:
 -
    fullname: Pieter Kasselman
    organization: Defakto Security
    email: "pieter@defakto.security"
 -
    fullname: Jean-François Lombardo
    organization: AWS
    email: jeffsec@amazon.com
 -
    fullname: Yaroslav Rosomakho
    organization: Zscaler
    email: yrosomakho@zscaler.com

normative:
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
  SPIFFE-ID:
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
  RFC7591:
    title: "OAuth 2.0 Dynamic Client Registration Protocol"
    target: https://datatracker.ietf.org/doc/html/rfc7591
  RFC7662:
    title: OAuth 2.0 Token Introspection
    target: https://datatracker.ietf.org/doc/rfc7662
  RFC9701:
    title: JWT Response for OAuth 2.0 Token Introspection
    target: https://datatracker.ietf.org/doc/rfc9701
  RFC8414:
    title: OAuth 2.0 Authorization Server Metadata
    target: https://datatracker.ietf.org/doc/html/rfc8414
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
    target: https://datatracker.ietf.org/doc/html/rfc8705
  OAuth.step-up.Auth-RFC9470:
    title: OAuth 2.0 Step Up Authentication Challenge Protocol
    target: https://www.rfc-editor.org/rfc/rfc9470.html
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
  OpenIDConnect.Discovery:
    title: OpenID Connect Discovery 1.0
    target: https://openid.net/specs/openid-connect-discovery-1_0-final.html
  OpenIDConnect.CIBA:
    title: OpenID Connect Client-Initiated Backchannel Authentication Flow - Core 1.0
    target: https://openid.net/specs/openid-client-initiated-backchannel-authentication-core-1_0.html
  OAuth.SPIFFE.Client.Auth:
    title: OAuth SPIFFE Client Authentication
    target: https://datatracker.ietf.org/doc/draft-ietf-oauth-spiffe-client-auth
  OAuth.CIMD:
    title: OAuth Client ID Metadata Document
    target: https://datatracker.ietf.org/doc/draft-ietf-oauth-client-id-metadata-document
  OAuth.IDJAG:
    title: Identity Assertion JWT Authorization Grant
    target: https://datatracker.ietf.org/doc/draft-ietf-oauth-identity-assertion-authz-grant/01/
  OAuth.IDChaining:
    title: OAuth Identity and Authorization Chaining Across Domains
    target: https://datatracker.ietf.org/doc/draft-ietf-oauth-identity-chaining/
  MCP:
    title: Model Context Protocol
    target: https://modelcontextprotocol.io/specification
  SSF:
    title: OpenID Shared Signals Framework Specification 1.0
    target: https://openid.net/specs/openid-sharedsignals-framework-1_0-final.html
  CAEP:
    title: OpenID Continuous Access Evaluation Profile 1.0
    target: https://openid.net/specs/openid-caep-1_0-final.html
  A2A:
    title: Agent2Agent (A2A) Protocol
    target: https://github.com/a2aproject/A2A
  ACP:
    title: Agentic Commerce Protocol
    target: https://www.agenticcommerce.dev/docs
  AP2:
    title: Agent Payments Protocol (AP2)
    target: https://github.com/google-agentic-commerce/AP2

informative:

...

--- abstract

This document proposes a framework for authentication and authorization of AI agent interactions. It leverages existing standards such as the Workload Identity Management and Secure Exchange (WIMSE) architecture and OAuth 2.0 family of specifications. Rather than defining new protocols, this document describes how existing and widely deployed standards can be applied or extended to establish agent authentication and authorization. By doing so, it aims to provide a framework within which to use existing standards, identify gaps and guide future standardization efforts for agent authentication and authorization.

--- middle

# Introduction

TODO Introduction


# Conventions and Definitions

{::boilerplate bcp14-tagged}

# Agents are workloads
An Agent is a workload that iteratively interacts with a Large Language Model (LLM) and a set of Tools, Services and Resources. An agent performs its operations until a terminating condition, determined either by the LLM or by the agent's internal logic, is reached. It may receive input from a user, or act autonomously. {{fig-ai-agent-workload}} shows a conceptual model of the AI Agent as a workload and illustrates the high-level interaction model between the User or System, the AI Agent, the Large Language Model (LLM), Tools, Services, and Resources.

In this document, Tools, Services, and Resources are treated as a single category of external endpoints that an agent invokes or interacts with to complete a task. Communication within or between Tools, Services, and Resources is out of scope.

~~~aasvg
                +----------------+
                | Large Language |
                |   Model (LLM)  |
                +----------------+
                      ▲   |
                     (2) (3)
                      |   ▼
+--------+       +------------+       +-----------+
|  User  |──(1)─►|  AI Agent  |──(4)─►|   Tools   |
|   or   |       | (workload) |       | Services  |
| System |◄─(6)──|            |◄─(5)──| Resources |
+--------+       +------------+       +-----------+
~~~
{: #fig-ai-agent-workload title="AI Agent as a Workload"}

1. Optional: The User or System (e.g. a batch job or another Agent) provides an initial request or instruction to the AI Agent.
2. The AI Agent provides the available context to the LLM. Context is implementation- and deployment-specific and may include User or System input, system prompts, Tool descriptions, prior Tool, Service and Resource outputs, and other relevant state.
3. The LLM returns output to the AI Agent facilitating selection of Tools, Services or Resources to invoke.
4. The AI Agent invokes one or more external endpoints of selected Tools, Services or Resources. A Tool endpoint may itself be implemented by another AI agent.
5. The external endpoint of the Tools, Services or Resources returns a result of the operation to the AI Agent, which may sends the information as additional context to the Large Language Model, repeating steps 2-5 until the exit condition is reached and the task is completed.
6. Optional: Once the exit condition is reached in step 5, the AI Agent may return a response to the User or System. The AI Agent may also return intermediate results or request additional input.

As shown in {{fig-ai-agent-workload}}, the AI Agent is a workload that needs an identifier and credentials with which it can be authenticated by the User or System, Large Language Model and Tools/Services/Resources. Once authenticated, these parties must determine if the AI Agent is authorized to access the requested Large Language Model, Tools, Services or Resources. If the AI Agent is acting on behalf of a User or System, the User or System needs to delegate authority to the AI Agent, and the User or System context MUST be preserved to as input to authorization decisions and recorded in audit trails.

This document describes how AI Agents should leverage existing standards defined by SPIFFE {{SPIFFE}}, WIMSE, OAuth and OpenID SSF {{SSF}}.

# Agent Identity Management System
This document defines the term Agent Identity Management System (AIMS) as a conceptual model describing the set of functions required to establish, maintain, and evaluate the identity and permissions of an agent workload. AIMS does not refer to a single product, protocol, or deployment architecture. AIMS may be implemented by one component or distributed across multiple systems (such as identity providers, attestation services, authorization servers, policy engines, and runtime enforcement points).

An Agent Identity Management System ensures that the right Agent has access to the right resources and tools at the right time for the right reason. An Agent identity management system depends on the following components to achieve its goals:

* **Agent Identifiers:** Unique identifier assigned to every Agent.
* **Agent Credentials:** Cryptographic binding between the Agent Identifier and attributes of the Agent.
* **Agent Attestation:** Mechanisms for determining and assigning the identifier and issue credentials based on measurements of the Agent's environment.
* **Agent Credential Provisioning:** The mechanism for provisioning credentials to the agent at runtime.
* **Agent Authentication:** Protocols and mechanisms used by the Agent to authenticate itself to Large Langugage Models or Tools (resource or server) in the system.
* **Agent Authorization:** Protocols and systems used to determine if an Agent is allowed to access a Large Langugage Model or Tool (resource or server).
* **Agent Monitoring and Remediation:** Protocols and mechanisms to dynamically modify the authorization decisions based on observed behaviour and system state.
* **Agent Auhtentication and Authorization Policy:** The configuration and rules for each of the Agent Identity Management System.
* **Agent Compliance:** Measurement of the state and fucntioning of the system against the stated policies.

The components form a logical stack in which higher layers depend on guarantees provided by lower layers, as illustrated in {{fig-agent-identity-management-system}}.

~~~aasvg
+--------------+----------------------------------+--------------+
|    Policy    |   Monitoring & Remediation       |  Complaince  |
|              +----------------------------------+              |
|              |          Authorization           |              |
|              +----------------------------------+              |
|              |          Authentication          |              |
|              +----------------------------------+              |
|              |          Provisioning            |              |
|              +----------------------------------+              |
|              |           Attestation            |              |
|              +----------------------------------+              |
|              |           Credentials            |              |
|              +----------------------------------+              |
|              |           Identifier             |              |
+--------------+----------------------------------+--------------+
~~~
{: #fig-agent-identity-management-system title="Agent Identity Management System"}

# Agent Identifier {#agent_identifiers}
Agents MUST be uniquely identified in order to support authentication, authorization, auditing, and delegation.

The Workload Identity in Multi-System Environments (WIMSE) identifier as defined by {{!WIMSE-ID=I-D.ietf-wimse-identifier}} is the canonical identifier for agents in this framework.

A WIMSE identifier is a URI that uniquely identifies a workload within a trust domain. Authorization decisions, delegation semantics, and audit records rely on this identifier remaining stable for the lifetime of the workload identity.

The Secure Production Identity Framework for Everyone ({{SPIFFE}}) identifier is a widely deployed and operationally mature implementation of the WIMSE identifier model. A SPIFFE identifier ({{SPIFFE-ID}}) is a URI in the form of `spiffe://<trust-domain>/<path>` that uniquely identifies a workload within a trust domain.

An agent participating in this framework MUST be assigned exactly one WIMSE identifier, which MAY be a SPIFFE ID.

# Agent Credentials {#agent_credentials}
Agents MUST possess credentials that provide a cryptographic binding to the agent identifier. These credentials are considered primary credentials that are provisioned at runtime. An identifier alone is insufficient unless it can be verified to be controlled by the communicating agent through a cryptographic binding.

WIMSE credentials ({{!WIMSE-CRED=I-D.ietf-wimse-workload-creds}}) are defined as a profile of X.509 certificates and Workload Identity Tokens (WITs), while SPIFFE defines SPIFFE Verified ID (SVID) profiles of JSON Web Token (JWT-SVID), X.509 certificates (X.509-SVID) and WIMSE Workload Identity Tokens (WIT-SVID). SPIFFE SVID credentials are compatible with WIMSE defined credentials. The choice of an appropriate format depends on the trust model and integration requirements.

Agent credentials SHOULD be short-lived to minimize the risk of credential theft, MUST include an explicit expiration time after which it is no longer accepted, and MAY carry additional attributes relevant to the agent (for example trust domain, attestation evidence, or workload metadata).

Deployments can improve the assurance of agent identity by protecting private keys using hardware-backed or isolated cryptographic storage such as TPMs, secure enclaves, or platform security modules when such capabilities are available. These mechanisms reduce key exfiltration risk but are not required for interoperability.

In some cases, agents MAY need a secondary credentials to access a proprietary or legacy system that is not compatible with the X.509, JWT or WIT it is provisioned with. In these cases an agent MAY exchange their primary credentials through a credential exchange mechanisms (e.g., OAuth 2.0 Token Exchange {{!OAUTH-TOKEN-EXCHANGE=RFC8693}}, Transaction Tokens {{!OAUTH-TRANS-TOKENS=I-D.ietf-oauth-transaction-tokens}} or Workload Identity Federation). This allows an agent to obtain a credential targeted to a specific relying party by leveraging the primary credential in its possession.

**Note**: Static API keys are an anti-pattern for agent identity. They are bearer artefacts that are not cryptographically bound, do not convey identity, are typically long-lived and are operationally difficult to rotate, making them unsuitable for secure agent authentication or authorization.

# Agent Attestation {#agent_attestation}
Agent attestation is the identity-proofing mechanism for AI agents. Just as humans rely on identity proofing during account creation or credential issuance, agents require a means to demonstrate what they are, how they were instantiated, and under what conditions they are operating. Attestation evidence feeds into the credential issuance process and determines whether a credential is issued, the type of credential issued and the contents of the credential.

Multiple attestation mechanisms exist, and the appropriate choice is deployment and risk specific. These mechanisms may include hardware-based attestations (e.g., TEE evidence), software integrity measurements, supply-chain provenance, platform and orchestration-layer attestations, or operator assertions to name a few. Depending on the risk involved, a single attestation may be sufficient, or, in higher risk scenarios, multi-attestation may be requred.

There are numerous systems that perform some kind of attestation, any of which can be used in establishing agent identity. One example of such a system is the Remote ATtestation Procedures (RATS) architecture ({{!RATS-ARCH=RFC9334}}), which provides a general model for producing, conveying, and verifying attestation evidence and defines the roles of Attester, Verifier, and Relying Party, as well as the concept of Evidence, Endorsements, and Attestation Results.

An agent identity management system may incorporate different attestation mechanisms and implementations (including RATS) to collect attestation evidence and provide it to credential provisioning components. The selection of mechanisms depends on the deployment constraints and the desired level of trust assurance.

# Agent Credential Provisioning {#agent_credential_provisioning}
Agent credential provisioning refers to the runtime issuance, renewal, and rotation of the credentials an agent uses to authenticate and authorize itself to other agents. Agents may be provisioned with one or more credential types as described in {{agent_credentials}}. Unlike static secrets, agent credentials are provisioned dynamically and are intentionally short-lived, eliminating the operational burden of manual expiration management and reducing the impact of credential compromise. Agent credential provisioning must operate autonomously, scale to high-churn environments, and integrate closely with the attestation mechanisms that establish trust in the agent at each issuance or rotation event.

Agent credential provisioning typically includes two phases:

1. **Initial Provisioning**: The process by which an agent first acquires a credential bound to its identity. This often occurs immediately after deployment or instantiation and is based on verified properties of the agent (e.g., deployment context, attestation evidence, or orchestration metadata).
2. **Rotation/Renewal**: The automatic refresh of short-lived credentials before expiration. Continuous rotation ensures that credentials remain valid only for the minimum necessary time and that authorization state reflects current operational conditions.

The use of short-lived credentials provides a signiifcant improvement in the risk profile and risk of credential exposure. It provides an alternative to explicit revocation mechanisms and simplifies lifecycle management in large, automated environments while removing the risks of downtime as a result of credential expiry.

Deployed frameworks such as {{SPIFFE}} provide proven mechanisms for automated, short-lived credential provisioning at runtime. In addition to issuing short-lived credentials, {{SPIFFE}} also provisions ephemeral cryptographic key material bound to each credential, further reducing the risks associated with compromising long-lived keys.

# Agent Authentication {#agent_authentication}
Agents may authenticate to one another using a variety of mechanisms, depending on the credentials they possess, the protocols supported in the deployment environment, and the risk profile of the application. As described in the WIMSE Architecture {{WIMSE_ARCH}}, authentication can occur at either the network layer or the application layer, and many deployments rely on a combination of both.

## Network layer authentication
Network-layer authentication establishes trust during the establishment of a secure transport channel. The most common mechanism used by agents is mutual TLS (mTLS), in which both endpoints present X.509-based credentials and perform a bidirectional certificate exchange as part of the TL negotiation. When paired with short-lived workload identities, such as those issued by SPIFFE or WIMSE, mTLS provides strong channel binding and cryptographic proof of control over the agent’s private key.

mTLS is particularly well-suited for environments where transport-level protection, peer authentication, and ephemeral workload identity are jointly required. It also simplifies authorization decisions by enabling agents to associate application-layer requests with an authenticated transport identity. One example of this is the use of mTLS in service mesh architecctures such as Istio or LinkerD.

**Limitations** There are scenarios where transport-layer authentication is not desirable or cannot be relied upon. In architectures involving intermediaries, such as API gateways, service meshes, load balancers, or protocol translators, TLS sessions are often terminated and re-established, breaking the end-to-end continuity of transport-layer identity. Similarly, some deployment models (e.g., serverless platforms, multi-tenant edge environments, or cross-domain topologies) may obscure or abstract identity presented at the transport layer, making it difficult for relying parties to bind application-layer actions to a credential presented at the transport-layer. In these cases, application-layer authentication provides a more robust and portable mechanism for expressing agent identity and conveying attestation or policy-relevant attributes.

## Application layer authentication
Application-layer authentication allows agents to authenticate independently of the underlying transport. This enables end-to-end identity preservation even when requests traverse proxies, load balancers, or protocol translation layers.

The WIMSE working group defines the following authentication mechanisms that may be used by agents:

### WIMSE Proof Tokens (WPTs) {#wpt}
WIMSE Workload Proof Tokens (WPTs) are a protocol-independent, application-layer mechanism for proving possession of the private key associated with a Workload Identity Token (WIT). WPTs are generated by the agent, using the private key matching the public key in the WIT. A WPT is defined as a signed JSON Web Token (JWT) that binds an agent’s authentication to a specific message context, for example, an HTTP request, thereby providing proof of possession rather than relying on bearer semantics {{WIMSE_WPT}}.

WPTs are designed to work alongside WITs {{WIMSE-CRED}} and are typically short-lived to reduce the window for replay attacks.  They carry claims such as audience (aud), expiration (exp), a unique token identifier (jti), and a hash of the associated WIT (wth). A WPT may also include hashes of other related tokens (e.g., OAuth access tokens) to bind the authentication contexts to specific transaction or authorizations details.

Although the draft currently defines a protocol binding for HTTP (via a Workload-Proof-Token header), the core format is protocol-agnostic, making it applicable to other protocols. Its JWT structure and claims model allow WPTs to be bound to different protocols and transports, including asynchronous or non-HTTP messaging systems such as Kafka and gRPC, or other future protocol bindings. This design enables relying parties to verify identity, key possession, and message binding at the application layer even in environments where transport-layer identity (e.g., mutual TLS) is insufficient or unavailable.

###  HTTP Message Signatures (HTTP Sig)
The WIMSE Workload-to-Workload Authentication with HTTP Signatures specification {{WIMSE_HTTPSIG}} defines an application-layer authentication profile built on the HTTP Message Signatures standard {{RFC9421}}. It is one of the mechanisms WIMSE defines for authenticating workloads in HTTP-based interactions where transport-layer protections may be insufficient or unavailable. The protocol combines a workload’s Workload Identity Token (WIT), which conveys attested identity and binds a public key, with HTTP Message Signatures using the corresponding private key, thereby providing proof of possession and message integrity for individual HTTP requests and responses. This approach ensures end-to-end authentication and integrity even when traffic traverses intermediaries such as TLS proxies or load balancers that break transport-layer identity continuity. The profile mandates signing of key request components (e.g., method, target, content digest, and the WIT itself) and supports optional response signing to ensure full protection of workload-to-workload exchanges.

# Agent Authorization {#agent_authorization}
Agents act on behalf of a user, a system, or on their own behalf as shown in {{fig-ai-agent-workload}} and needs to obtain authorization when interacting with protected resources.

## Leverage OAuth 2.0 as a Delegation Authorization Framework
The OAuth 2.0 Authorization Framework {{RFC6749}} is widely deployed and defines an authorization delegation framework that enables an Agent to obtain limited access to a protected resource (e.g. a service or API) under well-defined policy constraints. An Agent MUST use OAuth 2.0-based mechanisms to obtain authorization from a user, a system, or on its own behalf. OAuth 2.0 defines a wide range of authorization grant flows that supports these scenarios. In these Oauth 2.0 flows, an Agent acts as an OAuth 2.0 Client to an OAuth 2.0 Authorization Server, which receives the request, evaluate the authorization policy and returns an access token, which the Agent presents to the Resource Server (i.e. the protected resources such as the LLM or Tools in {{fig-ai-agent-workload}}) it needs to access to complete the request.

## Use of OAuth 2.0 Access Tokens
An OAuth access token represents the authorization granted to the Agent. In many deployments, access tokens are structured as JSON Web Tokens (JWTs) {{RFC9068}}, which include claims such as 'client_id', 'sub', 'aud', 'scope', and other attributes relevant to authorization. The access token MUST include the Agent identity as the 'client_id' claim as defined in Section 2.2 of {{RFC9068}}.

If the Agent is acting on-behalf of another user or system, it MUST include the user or system identifier in the 'sub' claim as defined in Section 2.2 of {{RFC9068}}. These identitifiers MUST be used by resource servers protected by the OAuth 2.0 authorization service, along with other claims in the access token, to determine if access to a resource should be allowed. The acccess token MAY include additional claims to convey contextual, attestation-derived, or policy-related information that enables fine-grained access control. The resource server MAY use the access token and the information it contains along with other authorization systems (e.g. policy based, attribute based or role based authorization systems) when enforcing access. Where JWT access tokens are not used, opaque tokens may be issued and validated through introspection mechanisms. This framework supports both models and does not require a specific token format, provided that equivalent authorization semantics are maintained.

## Obtaining an OAuth 2.0 Access Token
Agents MUST obtain OAuth 2.0 accss tokens using standards OAuth 2.0 Authorization Flows.

### User Delegates Authorization
When a User grants authorization to an Agent to access one or more resources (Tools, LLMs), the Authorization Code Grant MUST be used as described in Section 4.1 of {{RFC6749}}.

### Agent Obtains Own Authorization {#agent_obtains_own_access_token}
Agents obtaining access tokens on their own behalf MUST use the Client Credentials Grant as described in Section 4.4 of {{RFC6749}} or the JWT Authorization Grant as described in section 2.1. of {{OAuth.Private.JWT.Auth-RFC7523}}. When using the Client Credentials Grant, the Agent MUST authenticate itself using one of the mechanisms described in {{agent_authentication}} and MUST NOT use static, long lived client secrets to authenticate.

### System Access to Agents
When Agents are invoked by a System (e.g. a batcch job, or another Agent), the System SHOULD treat the Agent as an OAuth protected resource. The System SHOULD obtain an access token using the same mechanisms defined for an Agent and then present the OAuth access token to the Agent. The Agent should validate the access token, including verifiying that the 'aud' claim of the access token includes the Agent. Once validated, the Agent SHOULD use OAuth 2.0 Token Exchange as defined in {{OAUTH-TOKEN-EXCHANGE}} to exchange the access token it received for a new access token to access. The Agent then uses the newly issued access token to access the protected resources (LLM or Tools) it needs to complete the request.

If a System invokes an Agent and does not treat the Agent as an OAuth protected resource, the Agent MUST obtain its own OAuth access token as described in {#agent_obtains_own_access_token}.

### OAuth 2.0 Security Best Practices
Agents MUST support the Best Current Practice for OAuth 2.0 Security as described in {{RFC9700}} when requesting acccess tokens.

## Risk reduction with Transaction Tokens {#trat-risk-reduction}
Resources servers, whether they are LLMs, Tools or Agents (in the Agent-to-Agent case) may be composed of multiple microservices that are invoked to complete a request. The access tokens presented to the Agent, LLM or Tools can typically be used with multiple transactions and consequently have broader scope than needed to complete any specific transaction. Passing the access token from one microservice to another within an Agent, LLM or the Tools invoked by the Agent increases the risk of token theft and replay attaccks. For example, an attacker may discover and access token passed between microservices in a log file or crash dump, exfiltrate it, and use it to invoke a new transaction with different parameters (e.g. increase the trnasaction amount, or invoke an unrelated call as part of executing a lateral move).

To avoid passing access tokens between microservices, the Agent, LLM or Tools SHOULD exchange the access token it receives for a transaction token, as defined in the Transaction Token specification as defined in {{OAUTH-TRANS-TOKENS}}. The transaction token allows for identity and auhtorization information to be passed along a call chain between microservices. The transaction token issuer enriches the transaction token with context of the caller that presented the access token (e.g. IP address etc), transaction context (transaction amount), identity information and a unique transaction identifier. This results in a dowscoped token that is bound to a specific transaction that cannot be used as an access token, with another transaction, or within the same transaction with modified transaction details (e.g. change in transaction amount). Transaction tokens are typically short lived, further lmiting the risk in case they are obtained by an attacker by liomiting the time window during which these tokens will be accepted.

A transaction token MAY be used to obtain an access token to call another service (e.g. another Agent, Tool or LLM) by using OAuth 2.0 Token Exchange as defined in {{OAUTH-TOKEN-EXCHANGE}}.

## Cross Domain Access
Agents often require access to resources that are protected by different OAuth 2.0 authorization servers. When the components in {{fig-ai-agent-workload}} are protected by different logical authorization servers, an Agent SHOULD use OAuth Identity and Authorization Chaining Across Domains as defined in {{OAuth.IDChaining}}, or a derived specification such as the Identity Assertion JWT Authorization Grant {{OAuth.IDJAG}}, to obtain an access token from the relevant authorization servers.

When using OAuth Identity and Authorization Chaining Across Domains ({{OAuth.IDChaining}}), an Agent SHOULD use the access token or transaction token it received to obtain a JWT authorization grant as described in section 2.3 of {{OAuth.IDChaining}} and then use the JWT authorization grant it receives to obtain an access token for the resource it is trying to access as defined in section 2.4 of {{OAuth.IDChaining}}.

When using the Identity Assertion JWT Authorization Grant {{OAuth.IDJAG}}, the identity assertion (e.g. the OpenID Connect ID Token or SAML assertion) for the target end-user is used to obtain a JWT assertion (ID-JAG) as described in section 4.3 of {{OAuth.IDJAG}}, which is then used to obtain an access token as described in section 4.4 of {{OAuth.IDJAG}}.

OAuth Identity and Authorization Chaining Across Domains ({{OAuth.IDChaining}}) provides a general mechanism for obtaining cross-domain access that can be used whether an identity assertion like a SAML or OpenID Connect token is available or not. The Identity Assertion JWT Authorization Grant {{OAuth.IDJAG}} is optimised for cases where an identity assertion like a SAML or OpenID Connect token is available from an identity provider that is trusted by all the OAuth authorization servers as it removes the need for the user to re-authenticate. This is typically used within enterprise deployments to simplify authorization delegation for multiple software-as-a-service offerings.

## Human in the Loop
An OAuth authorization server MAY conclude that the level of access to a resource that an Agent, LLM or Tool is requesting requires additional authorization from the User. When it determines that additional authorization is required, it SHOULD either decline the request or request additional authorization from the User by using the OpenID foundation Client Initiated Backchannel Authentication (CIBA). This will trigger a request to the user to grant additional authorization (e.g. through a push notification). Once the user grant authorization, the authorization server issues an access token to the Agent which it may then use to complete the task.

## Tool-to-Service Acccess
Tools expose interfaces to underlying services and resources. Access to the Tools SHOULD be controlled by OAuth which MAY be augmented by policy, attribute or role based authorization systems (amongst others). If the Tools are implemented as one or more microservices, it should use transaction tokens to reduce risk as described in {{trat-risk-reduction}} to avoid passing access tokens around within the Tool implementation.

Access from the Tools to the resources and services MAY be controlled through a variety of auhtorization mechanisms, includidng OAuth. If access is controlled through OAuth, the Tools SHOULD use OAuth 2.0 Token Exchange as defined in {{OAUTH-TOKEN-EXCHANGE}} to exchange the access token it received for a new access token to access the resource or service in question. If the Tool needs acces to a resource protected by an auhtorization server other than the Tool's own authorization server, it SHOULD use the OAuth Identity and Authorization Chaining Across Domains ({{OAuth.IDChaining}}) to obtain an access token from the authroization server protecting the resource it needs to access.

## OAuth 2.0 Discovery in Dynamic Environments
In dynamic Agent deployments (e.g., ephemeral workloads, multi-tenant services, and frequently changing endpoint topology), Agents and other participants MAY use OAuth discovery mechanisms to reduce static configuration and to bind runtime decisions to verifiable metadata.

### Authorization Server Capability Discovery
An Agent that needs to obtain tokens MAY discover authorization server endpoints and capabilities using OAuth 2.0 Authorization Server Metadata {{RFC8414}} and/or OpenID Connect Discovery {{OpenIDConnect.Discovery}}. This allows the Agent to learn the as issuer identifier, authorization and token endpoints, supported grant types, client authentication methods, signing keys (via jwks_uri), and other relevant capabilities without preconfiguring them.

### Protected Resource Capability Discovery
When an Agent is invoking a Tool, the Agent MAY use OAuth 2.0 Protected Resource Metadata {{RFC9728}} to discover how the resource is protected, including the resource identifier and the applicable Authorization Server(s) that protects Tool access. This enables an Agent to select the correct issuer/audience and token acquisition flow at runtime, even when resources are deployed or moved dynamically.

A Tool that atttempts to acccess and OAuth protected resource MAY use OAuth 2.0 Protected Resource Metadata {{RFC9728}} in a similar way as an Agent. Similarly, a System may use {{RFC9728}} when accessing an Agent.

### Client Capability Discovery
Other actors (e.g., Authorization Servers, registrars, or policy systems) may need to learn about any entities (System, Agent, Tool) that acts as OAuth clients. Where supported, they MAY use Client ID Metadata Documents {{OAuth.CIMD}}, which allow a client to host its metadata at a URL-valued client_id so that the relying party can retrieve client properties (e.g., redirect URIs, software statement, display information, and other registered client metadata) without prior bilateral registration.

As an alternative, entities acting as OAuth clients MAY register their capabilities with authroization servers as defined in the OAuth 2.0 Dynamic Client Registration Protocol {{RFC7591}}.

# Agent Monitoring and Remediation {#agent_monitoring_and_remediation}
Agents operate in environments where authorization state can change after an access decision is made. Authroization state may change as a result of policy updates, session termination, device posture changes or elevated risk signals. Implementations SHOULD treat authorization as continuously evaluated rather than a one-time check, and SHOULD include monitoring and remediation mechanisms to detect and communicate changes in authorization status at runtime.

Any particiapant in the system, including the Agent, Tool, System, LLM or other resources and service MAY subscribe to change notifications using eventing mechanisms such as the OpenID Shared Signals Framework {{SSF}} with the Continuous Access Evaluation Profile {{CAEP}} to receive security and authorization-relevant signals. Upon receipt of a relevant signal (e.g., session revoked, subject disabled, token replay suspected, risk elevated), the recipient SHOULD remediate by attenuating access, such as terminating local sessions, discarding cached tokens, re-acquiring tokens with updated constraints, reducing privileges, or re-running policy evaluation before continueing to allow acccess.

To support detection, investigation, and accountability, deployments SHOULD produce durable logs and audit trails for both authorization decisions and subsequent remediations. This includes recording the Agent, User, System,  LLM, resource or service identity, the targeted resource/tool, token identifiers or hashes, and the triggering signals that caused re-evaluation or revocation.

End-to-end audit is enabled when Agents, Users, Systems, LLMs, Tools, services and resources have stable, verifiable identifiers that allow auditors to trace “which entity did what, using which authorization context, and why access changed over time.”

# Agent Authentication and Authorization Policy {#agent_auhtentication_and_authorization_policy}
The configuration and runtime parameters for Agent Identifiers {{agent_identifiers}}, Agent Credentials {{agent_credentials}}, Agent Attestation {{agent_attestation}}, Agent Credential Provisioning {{agent_credential_provisioning}}, Agent Authentication {{agent_authentication}}, Agent Authorization {{agent_authorization}} and Agent Monitoring and Remediation {{agent_monitoring_and_remediation}} collectively constitute the authentication and authorization policy within which the Agent operates.

Because these parameters are highly deployment- and risk-model-specific (and often reflect local governance, regulatory, and operational constraints), the policy model and document format are out of scope for this framework and are not recommended as a target for standardization within this specification. Implementations MAY represent policy in any suitable “policy-as-code” or configuration format (e.g., JSON/YAML), provided it is versioned, reviewable, and supports consistent evaluation across the components participating in the end-to-end flow.

# Agent Compliance {#agent_compliance}
Compliance for Agent-based systems SHOULD be assessed by auditing observed behavior and recorded evidence (logs, signals, and authorization decisions) against the deployment’s Agent Authentication and Authorization Policy {{agent_auhtentication_and_authorization_policy}}. Since compliance criteria are specific to individual deployments, organizations, industries and jurisdictions, they are out of scope for this framework though implementers SHOULD ensure strong observability and accountable governance, subject to their specific business needs.

# Security Considerations

TODO Security

# Privacy Considerations

TODO Privac

# IANA Considerations

This document has no IANA actions.


-----------------------End of "High Level Map"------------------------------

-----------------------Early Thoughts on Detailed Spec Below------------------------------

# Agent Authorization - Next Level Detail

During Agent execution, authorization must be enforced at all the components involved in the process to provide an in-depth protection of the resources that might be interacted with. For each component, we must consider the following 3 phases:
- Negotiation between the component and its caller on the required pieces of authorization required to interact with the component
- Acquisition of the piece of authorization by the caller at the authorization server authoritative for the component it wants to communication
- Validation of the piece of authorization in the context of the request by the component

Those phases rely on the following standards for enforcement of the access control:
- {{RFC6749}} is an established and maintained framework of specifications for requesting, acquiring, and proving ownership of pieces of authorization in the form of bearer tokens.
- {{OpenIDConnect.AuthZEN}} is a new specification for exchanging authorization requests and decisions between the layer acting at the Policy Enforcement Point (PEP) and a Policy Decision Point (PDP).
- {{OAUTH-TRANS-TOKENS}} is new specification for formatting pieces of authorization in the form of transaction bound bearer tokens.

~~~ ascii-art
                       +----------------+
                       | Large Language |
                       |   Model (LLM)  |
                       +----------------+
                              ▲   |
                              │   |               ┌(H)┐
                              |   ▼               ▼   │
+--------------+         +------------+         +-------------+         +-----------+
|  User /      |─(A)(C)─►|  AI Agent  |─(E)(H)─►| Agent /     |─(J)(M)─►| Services  |
|      /       |         | (workload) |         |      /      |         |   and     |
|     / System |◄────────|            |◄────────|     / Tools |◄────────| Resources |
+--------------+         +------------+         +-------------+         +-----------+
     ▲                       ▲  ▲                   ▲   ▲                    ▲
     |    ┌──(F)─────────────┘  |                   |   |                    |
     |    |   ┌───(D)───────────┘                  (I)  |                    |
     |    |   |  +---------------+                  |  (K)                  (N)
    (B)   |   |  |    Policy     |                  |   |                    |
     |    |   └─►|   Decision    |◄─────────────────┘   |                    |
     |    |      |    Point      |◄─────────────────────┼────────────────────┘
     |    |      +---------------+                      |
     |    |             ▲                               |
     |    |          (G)(L)                             |
     |    |             ▼                               |
     |    |      +---------------+                      |
     |    └─────►| Authorization |◄─────────────────────┘
     └──────────►|   server      |
                 +---------------+
~~~


> Key point - OAuth is broadly supported and provides a delegation model for users to clients (aka Agents). Agents can obtain access tokens directly (client credentials flow, using above authentication methods) or it can be delegated to them by a user (OAuth flows). Make point that the access token includes the client_id, which is the same as the Agent ID (ore related to it) and can be used for authorization decisions, along with other claims in an Access Token (reference JWT Access token spec). Make provision for opaque tokens as well. Discuss Downscoping of Agent authorization using transaction tokens. Discuss cross-domain authorization (use cases) and how it may be achieved (identity chaining and cross-domain authorization). Discuss human in the loop authorization. Note concerns, refer to cross-device BCP as examples of consent phishing attacks. Talk about CIBA as a protocol.

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

## AI Agent To Other Agent / Tools

Interactions between an AI Agent and Tools are globally specified by {{MCP}}. Those sections only focus on the Identification, authentication, and authorization aspects of the specification.

Interactions between an AI Agent and other AI Agents are globally specified by {{A2A}}. Note that derived specifications and domain specific specification have emerged like {{AP2}} for Agent payment interaction, {{ACP}} for Agent to commerce flows. Those sections only focus on the Identification, authentication, and authorization aspects of those specifications.

### (E) Negotiation

#### Case of a Tool
Following {{MCP}}, the AI Agent MUST interact with Tools on the metadata endpoint of an OAuth 2.0 protected resource to understand which Authorization Server is the authority this resource; which scopes or authorization details values MAY be required to access this resources; and if proof of possession needs to be presented as standardized with {{RFC9449}}.

#### Case of an Agent

Following {{A2A}}, the AI Agent MUST interact with the other Agent through their Agent Card. If Extended Agent Card is implemented, the calling AI Agent MUST collect the information to understand which Authorization Server is the authority this resource; which scopes or authorization details values MAY be required to access this resources; and if proof of possession needs to be presented as standardized with {{RFC9449}}.

{{ACP}} and {{AP2}} Agents are expected to follow the same Agent Card feature as {{A2A}} Agents.

### (F) AI Agent Authorization

Based on the information collected as part of (E), the AI Agent is initiating an authorization request with the Authorization Server acting as authority for the AI Tools.

Such authorization request can allow to down, change or translate scope; enrich the authorization with new details based on the context; extend the time boundaries of the authorization; or change from a delegation mode to an impersonation mode and reversely.

- If the AI Agent acts on its behalf as a system:
  - If it does not want or need to refer to the previous context, it MUST start a client credential grant flow as described in section 1.3.4 of {{RFC6749}};
  - If it does want or need to refer to the previous context, it MUST start a token exchange flow as described in {{OAUTH-TOKEN-EXCHANGE}}. The AI Agent will be able to decide in between obtaining tokens representing a Delegation or an Impersonation as described in section 1.1 of the specification.
- If the AI Agent acts on delegation by a user:
  - If the AI Agent can interact and want to interact with the user through the client, it MUST start an authorization code grant flow as described in section 1.3.1 of {{RFC6749}};
  - If the AI Agent cannot or does not want to interact with the user through the client, it MAY:
    - Start a token exchange flow as described in {{OAUTH-TOKEN-EXCHANGE}}. The AI Agent will be able to decide in between obtaining tokens representing a Delegation or an Impersonation as described in section 1.1 of the specification.
    - Start a client initated backchannel authorized request as described in {{OpenIDConnect.CIBA}}

If the AI Agent knows that the underlying actions

> Transaction Tokens

### Security

If the metadata documents are cryptographically signed, the AI Agent MUST validate the signature before using the information for any authentication and authorization decision.

## Agent-to-Resource Authorization
Present token, peform additional authorization (RBAC etc?)
Direct or via tools
Resources, services.

Agent -> Tool -> Service -> Resource

### Human-in-the loop
Agent framework problem -> human in the loop - confirm something that it can already do - Agent framework capability - confirmation. Risk management flow.
Human in the loop - request esalated privelages. Step-up authorization - refernece the draft (maybe)

MCP Elicitation to Agent to perform some browser things - start authz code grant flow.
CIBA

## Case of Multi-Domain Authorization

### Cross Domain Agent-to-Agent Authorization
Identiyt chaining, ID-Jag.

## Agent to Agent Authorization


--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
