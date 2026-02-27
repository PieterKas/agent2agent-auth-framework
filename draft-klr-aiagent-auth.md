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
  SPIFFE:
    title: "Secure Production Identity Framework for Everyone"
    target: https://spiffe.io/docs/latest/spiffe-about/overview/
  SPIFFE-ID:
    title: SPIFFE-ID
    target: https://github.com/spiffe/spiffe/blob/main/standards/SPIFFE-ID.md
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

As shown in {{fig-ai-agent-workload}}, the AI agent is a workload that needs an identifier and credentials so it can be authenticated by the Tools, Services, Resources, Large Langugage Model, System and the User (via the underlying operating system or platform, similar to existing applications and services). Once authenticated, these parties must determine if the AI Agent is authorized to access the requested Large Language Model, Tools, Services or Resources. If the AI Agent is acting on behalf of a User or System, the User or System needs to delegate authority to the AI Agent, and the User or System context MUST be preserved to as input to authorization decisions and recorded in audit trails.

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

The Workload Identity in Multi-System Environments (WIMSE) identifier as defined by {{!WIMSE-ID=I-D.ietf-wimse-identifier}} is the primary identifier for agents in this framework.

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

There are numerous systems that perform some form of attestation, any of which can contribute to establishing agent identity. For example, SPIFFE implementations can attest workloads using platform and environment specific mechanisms. At a high level, an attesting component gathers workload and execution context signals (such as where the workload is running and relevant platform identity attributes), presents those signals for verification to an issuer, and, as long as verification succeeds, binds the workload to a SPIFFE identifier and issues credentials (such as SVID) for subsequent authentication and authorization.

An agent identity management system may incorporate multiple attestation mechanisms and implementations to collect evidence and supply it to credential provisioning components. The selection of mechanisms depends on deployment constraints (such as the underlying platform and available identity signals) and the desired level of trust assurance.

# Agent Credential Provisioning {#agent_credential_provisioning}
Agent credential provisioning refers to the runtime issuance, renewal, and rotation of the credentials an agent uses to authenticate and authorize itself to other agents. Agents may be provisioned with one or more credential types as described in {{agent_credentials}}. Unlike static secrets, agent credentials are provisioned dynamically and are intentionally short-lived, eliminating the operational burden of manual expiration management and reducing the impact of credential compromise. Agent credential provisioning must operate autonomously, scale to high-churn environments, and integrate closely with the attestation mechanisms that establish trust in the agent at each issuance or rotation event.

Agent credential provisioning typically includes two phases:

1. **Initial Provisioning**: The process by which an agent first acquires a credential bound to its identity. This often occurs immediately after deployment or instantiation and is based on verified properties of the agent (e.g., deployment context, attestation evidence, or orchestration metadata).
2. **Rotation/Renewal**: The automatic refresh of short-lived credentials before expiration. Continuous rotation ensures that credentials remain valid only for the minimum necessary time and that authorization state reflects current operational conditions.

The use of short-lived credentials provides a signiifcant improvement in the risk profile and risk of credential exposure. It provides an alternative to explicit revocation mechanisms and simplifies lifecycle management in large, automated environments while removing the risks of downtime as a result of credential expiry.

Deployed frameworks such as {{SPIFFE}} provide proven mechanisms for automated, short-lived credential provisioning at runtime. In addition to issuing short-lived credentials, {{SPIFFE}} also provisions ephemeral cryptographic key material bound to each credential, further reducing the risks associated with compromising long-lived keys.

# Agent Authentication {#agent_authentication}
Agents may authenticate using a variety of mechanisms, depending on the credentials they possess, the protocols supported in the deployment environment, and the risk profile of the application. As described in the WIMSE Architecture {{!WIMSE-ARCH=I-D.ietf-wimse-arch}}, authentication can occur at either the transport layer or the application layer, and many deployments rely on a combination of both.

## Transport layer authentication
Transport-layer authentication establishes trust during the establishment of a secure transport channel. The most common mechanism used by agents is mutually-authenticated TLS (mTLS), in which both endpoints present X.509-based credentials and perform a bidirectional certificate exchange as part of the TLS negotiation. When paired with short-lived workload identities, such as those issued by SPIFFE or WIMSE, mTLS provides strong channel binding and cryptographic proof of control over the agent’s private key.

mTLS is particularly well-suited for environments where transport-level protection, peer authentication, and ephemeral workload identity are jointly required. It also simplifies authorization decisions by enabling agents to associate application-layer requests with an authenticated transport identity. One example of this is the use of mTLS in service mesh architecctures such as Istio or LinkerD.

### Limitations
There are scenarios where transport-layer authentication is not desirable or cannot be relied upon. In architectures involving intermediaries, such as proxies, API gateways, service meshes, load balancers, or protocol translators, TLS sessions are often terminated and re-established, breaking the end-to-end continuity of transport-layer identity. Similarly, some deployment models (such as serverless platforms, multi-tenant edge environments, or cross-domain topologies) may obscure or abstract identity presented at the transport layer, making it difficult for relying parties to bind application-layer actions to a credential presented at the transport-layer. In these cases, application-layer authentication provides a more robust and portable mechanism for expressing agent identity and conveying attestation or policy-relevant attributes.

## Application layer authentication
Application-layer authentication allows agents to authenticate independently of the underlying transport. This enables end-to-end identity preservation even when requests traverse proxies, load balancers, or protocol translation layers.

The WIMSE working group defines WIMSE Proof Tokens and HTTP Message Signatures as authentication mechanisms that may be used by agents.

### WIMSE Proof Tokens (WPTs) {#wpt}
WIMSE Workload Proof Tokens (WPTs, {{!WIMSE-WPT=I-D.ietf-wimse-wpt}}) are a protocol-independent, application-layer mechanism for proving possession of the private key associated with a Workload Identity Token (WIT). WPTs are generated by the agent, using the private key matching the public key in the WIT. A WPT is defined as a signed JSON Web Token (JWT) that binds an agent’s authentication to a specific message context, for example, an HTTP request, thereby providing proof of possession rather than relying on bearer semantics.

WPTs are designed to work alongside WITs {{WIMSE-CRED}} and are typically short-lived to reduce the window for replay attacks.  They carry claims such as audience (aud), expiration (exp), a unique token identifier (jti), and a hash of the associated WIT (wth). A WPT may also include hashes of other related tokens (e.g., OAuth access tokens) to bind the authentication contexts to specific transaction or authorizations details.

Although the draft currently defines a protocol binding for HTTP (via a Workload-Proof-Token header), the core format is protocol-agnostic, making it applicable to other protocols. Its JWT structure and claims model allow WPTs to be bound to different protocols and transports, including asynchronous or non-HTTP messaging systems such as Kafka and gRPC, or other future protocol bindings. This design enables relying parties to verify identity, key possession, and message binding at the application layer even in environments where transport-layer identity (e.g., mutual TLS) is insufficient or unavailable.

### HTTP Message Signatures
The WIMSE Workload-to-Workload Authentication with HTTP Signatures specification {{!WIMSE-HTTPSIG=I-D.ietf-wimse-http-signature}} defines an application-layer authentication profile built on the HTTP Message Signatures standard {{!HTTP-SIG=RFC9421}}. It is one of the mechanisms WIMSE defines for authenticating workloads in HTTP-based interactions where transport-layer protections may be insufficient or unavailable. The protocol combines a workload's Workload Identity Token (WIT) (which binds the agent's identity to a public key) with HTTP Message Signatures (using the corresponding private key), thereby providing proof of possession and message integrity for individual HTTP requests and responses. This approach ensures end-to-end authentication and integrity even when traffic traverses intermediaries such as TLS proxies or load balancers that break transport-layer identity continuity. The profile mandates signing of critical request components (e.g., method, target, content digest, and the WIT itself) and supports optional response signing to ensure full protection of workload-to-workload exchanges.

### Limitations
Unlike transport-layer authentication, application-layer authentication does not inherently provide channel binding to the underlying secure transport. As a result, implementations MUST consider the risk of message relay or replay if tokens or signed messages are accepted outside their intended context. Deployments typically mitigate these risks through short token lifetimes, audience restrictions, nonce or unique identifier checks, and binding authentication to specific requests or transaction parameters.

# Agent Authorization {#agent_authorization}
Agents act on behalf of a user, a system, or on their own behalf as shown in {{fig-ai-agent-workload}} and needs to obtain authorization when interacting with protected resources.

## Leverage OAuth 2.0 as a Delegation Authorization Framework
The OAuth 2.0 Authorization Framework {{!OAUTH-FRAMEWORK=RFC6749}} is widely deployed and defines an authorization delegation framework that enables an Agent to obtain limited access to a protected resource (e.g. a service or API) under well-defined policy constraints. An Agent MUST use OAuth 2.0-based mechanisms to obtain authorization from a user, a system, or on its own behalf. OAuth 2.0 defines a wide range of authorization grant flows that supports these scenarios. In these Oauth 2.0 flows, an Agent acts as an OAuth 2.0 Client to an OAuth 2.0 Authorization Server, which receives the request, evaluate the authorization policy and returns an access token, which the Agent presents to the Resource Server (i.e. the protected resources such as the LLM or Tools in Figure 1) it needs to access to complete the request.

## Use of OAuth 2.0 Access Tokens
An OAuth access token represents the authorization granted to the Agent. In many deployments, access tokens are structured as JSON Web Tokens (JWTs) {{!OAUTH-ACCESSTOKEN-JWT=RFC9068}}, which include claims such as 'client_id', 'sub', 'aud', 'scope', and other attributes relevant to authorization. The access token MUST include the Agent identity as the 'client_id' claim as defined in {{Section 2.2 of OAUTH-ACCESSTOKEN-JWT}}.

If the Agent is acting on-behalf of another User or System, it MUST include the User or System identifier in the 'sub' claim as defined in {{Section 2.2 of OAUTH-ACCESSTOKEN-JWT}}. These identitifiers MUST be used by resource servers protected by the OAuth 2.0 authorization service, along with other claims in the access token, to determine if access to a resource should be allowed. The acccess token MAY include additional claims to convey contextual, attestation-derived, or policy-related information that enables fine-grained access control. The resource server MAY use the access token and the information it contains along with other authorization systems (e.g. policy based, attribute based or role based authorization systems) when enforcing access. Where JWT access tokens are not used, opaque tokens may be issued and validated through introspection mechanisms. This framework supports both models and does not require a specific token format, provided that equivalent authorization semantics are maintained.

When opaque tokens are used, the resource server MUST obtain authorization information through OAuth 2.0 Token Introspection {{!OAUTH-TOKEN-INTROSPECTION=RFC7662}}. The introspection response provides the active state of the token and associated authorization attributes equivalent to those conveyed in structured tokens.

## Obtaining an OAuth 2.0 Access Token
Agents MUST obtain OAuth 2.0 accss tokens using standards OAuth 2.0 Authorization Flows.

### User Delegates Authorization
When a User grants authorization to an Agent to access one or more resources (Tools, LLMs), the Authorization Code Grant MUST be used as described in {{Section 4.1 of OAUTH-FRAMEWORK}}.

### Agent Obtains Own Authorization {#agent_obtains_own_access_token}
Agents obtaining access tokens on their own behalf MUST use the Client Credentials Grant as described in {{Section 4.4 of OAUTH-FRAMEWORK}} or the JWT Authorization Grant as described in {{Section 2.1 of !OAUTH-CLIENTAUTH-JWT=RFC7523}}. When using the Client Credentials Grant, the Agent MUST authenticate itself using one of the mechanisms described in {{agent_authentication}} and MUST NOT use static, long lived client secrets to authenticate.

### System Access to Agents
When Agents are invoked by a System (e.g. a batch job, or another Agent), the System SHOULD treat the Agent as an OAuth protected resource. The System SHOULD obtain an access token using the same mechanisms defined for an Agent and then present the OAuth access token to the Agent. The Agent should validate the access token, including verifiying that the 'aud' claim of the access token includes the Agent. Once validated, the Agent SHOULD use OAuth 2.0 Token Exchange as defined in {{!OAUTH-TOKEN-EXCHANGE=RFC8693}} to exchange the access token it received for a new access token to access. The Agent then uses the newly issued access token to access the protected resources (LLM or Tools) it needs to complete the request.

If a System invokes an Agent and does not treat the Agent as an OAuth protected resource, the Agent MUST obtain its own OAuth access token as described in {{agent_obtains_own_access_token}}.

### OAuth 2.0 Security Best Practices
Agents MUST support the Best Current Practice for OAuth 2.0 Security as described in {{!OAUTH-BCP=RFC9700}} when requesting acccess tokens.

## Risk reduction with Transaction Tokens {#trat-risk-reduction}
Resources servers, whether they are LLMs, Tools or Agents (in the Agent-to-Agent case) may be composed of multiple microservices that are invoked to complete a request. The access tokens presented to the Agent, LLM or Tools can typically be used with multiple transactions and consequently have broader scope than needed to complete any specific transaction. Passing the access token from one microservice to another within an Agent, LLM or the Tools invoked by the Agent increases the risk of token theft and replay attaccks. For example, an attacker may discover and access token passed between microservices in a log file or crash dump, exfiltrate it, and use it to invoke a new transaction with different parameters (e.g. increase the trnasaction amount, or invoke an unrelated call as part of executing a lateral move).

To avoid passing access tokens between microservices, the Agent, LLM or Tools SHOULD exchange the access token it receives for a transaction token, as defined in the Transaction Token specification as defined in {{OAUTH-TRANS-TOKENS}}. The transaction token allows for identity and auhtorization information to be passed along a call chain between microservices. The transaction token issuer enriches the transaction token with context of the caller that presented the access token (e.g. IP address etc), transaction context (transaction amount), identity information and a unique transaction identifier. This results in a dowscoped token that is bound to a specific transaction that cannot be used as an access token, with another transaction, or within the same transaction with modified transaction details (e.g. change in transaction amount). Transaction tokens are typically short lived, further lmiting the risk in case they are obtained by an attacker by liomiting the time window during which these tokens will be accepted.

A transaction token MAY be used to obtain an access token to call another service (e.g. another Agent, Tool or LLM) by using OAuth 2.0 Token Exchange as defined in {{OAUTH-TOKEN-EXCHANGE}}.

## Cross Domain Access
Agents often require access to resources that are protected by different OAuth 2.0 authorization servers. When the components in {{fig-ai-agent-workload}} are protected by different logical authorization servers, an Agent SHOULD use OAuth Identity and Authorization Chaining Across Domains as defined in ({{!OAUTH-ID-CHAIN=I-D.ietf-oauth-identity-chaining}}), or a derived specification such as the Identity Assertion JWT Authorization Grant {{!OAUTH-JWT-ASSERTION=I-D.ietf-oauth-identity-assertion-authz-grant}}, to obtain an access token from the relevant authorization servers.

When using OAuth Identity and Authorization Chaining Across Domains ({{OAUTH-ID-CHAIN}}), an Agent SHOULD use the access token or transaction token it received to obtain a JWT authorization grant as described in {{Section 2.3 of OAUTH-ID-CHAIN}} and then use the JWT authorization grant it receives to obtain an access token for the resource it is trying to access as defined in {{Section 2.4 of OAUTH-ID-CHAIN}}.

When using the Identity Assertion JWT Authorization Grant {{OAUTH-JWT-ASSERTION}}, the identity assertion (e.g. the OpenID Connect ID Token or SAML assertion) for the target end-user is used to obtain a JWT assertion as described in {{Section 4.3 of OAUTH-JWT-ASSERTION}}, which is then used to obtain an access token as described in {{Section 4.4 of OAUTH-JWT-ASSERTION}}.

OAuth Identity and Authorization Chaining Across Domains ({{OAUTH-ID-CHAIN}}) provides a general mechanism for obtaining cross-domain access that can be used whether an identity assertion like a SAML or OpenID Connect token is available or not. The Identity Assertion JWT Authorization Grant {{OAUTH-JWT-ASSERTION}} is optimised for cases where an identity assertion like a SAML or OpenID Connect token is available from an identity provider that is trusted by all the OAuth authorization servers as it removes the need for the user to re-authenticate. This is typically used within enterprise deployments to simplify authorization delegation for multiple software-as-a-service offerings.

## Human in the Loop
An OAuth authorization server MAY conclude that the level of access requested by an Agent requires explicit user confirmation. In such cases the authorization server SHOULD either decline the request or obtain additional authorization from the User using the OpenID Client Initiated Backchannel Authentication (CIBA) protocol. This triggers an out-of-band interaction allowing the user to approve or deny the requested operation without exposing credentials to the agent (for example a push notification requesting the user to approve a request through an authenticator application on their mobile device).

Interactive agent frameworks may also solicit user confirmation directly during task execution (for example tool invocation approval or parameter confirmation). Such interactions do not by themselves constitute authorization and MUST be bound to a verifiable authorization grant issued by the authorization server. The agent SHOULD therefore translate user confirmation into an OAuth authorization event (e.g., step-up authorization via CIBA) before accessing protected resources.

This model aligns with user-solicitation patterns such as those described by the Model Context Protocol ({{MCP}}), where an agent pauses execution and requests user confirmation before performing sensitive actions. The final authorization decision remains with the authorization server, and the agent MUST NOT treat local UI confirmation alone as sufficient authorization.

## Tool-to-Service Acccess
Tools expose interfaces to underlying services and resources. Access to the Tools SHOULD be controlled by OAuth which MAY be augmented by policy, attribute or role based authorization systems (amongst others). If the Tools are implemented as one or more microservices, it should use transaction tokens to reduce risk as described in {{trat-risk-reduction}} to avoid passing access tokens around within the Tool implementation.

Access from the Tools to the resources and services MAY be controlled through a variety of auhtorization mechanisms, includidng OAuth. If access is controlled through OAuth, the Tools SHOULD use OAuth 2.0 Token Exchange as defined in {{OAUTH-TOKEN-EXCHANGE}} to exchange the access token it received for a new access token to access the resource or service in question. If the Tool needs access to a resource protected by an auhtorization server other than the Tool's own authorization server, it SHOULD use the OAuth Identity and Authorization Chaining Across Domains ({{OAUTH-ID-CHAIN}}) to obtain an access token from the authroization server protecting the resource it needs to access.

**Note:** It is an anti-pattern for Tools to forward access tokens it received from the Agent to Services or Resources. It increases the risk of credential theft and lateral attacks.

## Privacy Considerations
Authorization tokens may contain user identifiers, agent identifiers, audience restrictions, transaction details, and contextual attributes. Deployments SHOULD minimize disclosure of personally identifiable or sensitive information in tokens and prefer audience-restricted and short-lived tokens. Where possible, opaque tokens with introspection SHOULD be preferred when claim minimization is required.

Agents SHOULD request only the minimum scopes and authorization details necessary to complete a task. Resource servers SHOULD avoid logging full tokens and instead log token identifiers or hashes. When authorization context is propagated across services, derived or down-scoped tokens (such as transaction tokens) SHOULD be used to reduce correlation and replay risk.

Implementations MUST ensure that user identity information delegated to agents is not exposed to unrelated services and that cross-domain authorization exchanges only disclose information required for the target authorization decision.

## OAuth 2.0 Discovery in Dynamic Environments
In dynamic Agent deployments (e.g., ephemeral workloads, multi-tenant services, and frequently changing endpoint topology), Agents and other participants MAY use OAuth discovery mechanisms to reduce static configuration and to bind runtime decisions to verifiable metadata.

### Authorization Server Capability Discovery
An Agent that needs to obtain tokens MAY discover authorization server endpoints and capabilities using OAuth 2.0 Authorization Server Metadata {{!OAUTH-SERVER-METADATA=RFC8414}} and/or OpenID Connect Discovery {{OpenIDConnect.Discovery}}. This allows the Agent to learn the as issuer identifier, authorization and token endpoints, supported grant types, client authentication methods, signing keys (via jwks_uri), and other relevant capabilities without preconfiguring them.

### Protected Resource Capability Discovery
When an Agent is invoking a Tool, the Agent MAY use OAuth 2.0 Protected Resource Metadata {{!OAUTH-RESOURCE-METADATA=RFC9728}} to discover how the resource is protected, including the resource identifier and the applicable Authorization Server(s) that protects Tool access. This enables an Agent to select the correct issuer/audience and token acquisition flow at runtime, even when resources are deployed or moved dynamically.

A Tool that atttempts to acccess and OAuth protected resource MAY use OAuth 2.0 Protected Resource Metadata {{OAUTH-RESOURCE-METADATA}} in a similar way as an Agent. Similarly, a System may use {{OAUTH-RESOURCE-METADATA}} when accessing an Agent.

### Client Capability Discovery
Other actors (e.g., Authorization Servers, registrars, or policy systems) may need to learn about any entities (System, Agent, Tool) that acts as OAuth clients. Where supported, they MAY use Client ID Metadata Documents {{!OAUTH-CLIENT-METADATA=I-D.ietf-oauth-client-id-metadata-document}}, which allow a client to host its metadata at a URL-valued client_id so that the relying party can retrieve client properties (e.g., redirect URIs, software statement, display information, and other registered client metadata) without prior bilateral registration.

As an alternative, entities acting as OAuth clients MAY register their capabilities with authroization servers as defined in the OAuth 2.0 Dynamic Client Registration Protocol {{!OAUTH-REGISTRATION=RFC7591}}.

# Agent Monitoring and Remediation {#agent_monitoring_and_remediation}
Because agents may perform sensitive actions autonomously or on behalf of users, deployments MUST maintain sufficient observability to reconstruct agent behavior and authorization context after execution. Monitoring is therefore a security control, not solely an operational feature.

Any particiapant in the system, including the Agent, Tool, System, LLM or other resources and service MAY subscribe to change notifications using eventing mechanisms such as the OpenID Shared Signals Framework {{SSF}} with the Continuous Access Evaluation Profile {{CAEP}} to receive security and authorization-relevant signals. Upon receipt of a relevant signal (e.g., session revoked, subject disabled, token replay suspected, risk elevated), the recipient SHOULD remediate by attenuating access, such as terminating local sessions, discarding cached tokens, re-acquiring tokens with updated constraints, reducing privileges, or re-running policy evaluation before continueing to allow acccess. Recipients of such signals MUST ensure that revoked or downgraded authorization is enforced without undue delay. Cached authorization decisions and tokens that are no longer valid MUST NOT continue to be used after a revocation or risk notification is received.

To support detection, investigation, and accountability, deployments MUST produce durable audit logs covering authorization decisions and subsequent remediations. Audit records MUST be tamper-evident and retained according to the security policy of the deployment.

At a minimum, audit events MUST record:

* authenticated agent identifier
* delegated subject (user or system), when present
* resource or tool being accessed
* action requested and authorization decision
* timestamp and transaction or request correlation identifier
* attestation or risk state influencing the decision
* remediation or revocation events and their cause

Monitoring systems SHOULD correlate events across Agents, Tools, Services, Resources and LLMs to detect misuse patterns such as replay, confused deputy behavior, privilege escalation, or unexpected action sequences.

End-to-end audit is enabled when Agents, Users, Systems, LLMs, Tools, services and resources have stable, verifiable identifiers that allow auditors to trace "which entity did what, using which authorization context, and why access changed over time."

Implementations SHOULD provide operators the ability to reconstruct a complete execution chain of an agent task, including delegated authority, intermediate calls, and resulting actions across service boundaries.

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

--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
