Requests to interact with the cluster go through [[API Server]].

Requests must pass through three layers of security:
1. Authentication establishes the identity of the issuer of the request.
2. Authorization verifies that the authenticated requestor can perform the requested activity.
3. Admission control is a suite of software modules that validate and/or modify the request.

There are two types of users:
1. Normal users are managed outside of the cluster, however you like.
2. Service accounts allow in-cluster processes to interact with the [[API Server]]

Available authentication strategies include:
- X509 client certificates, provided the API server has a certificate authority on file
- Static file of valid bearer tokens
- Service account bearer tokens, for giving in-cluster processes access to the API server
- OpenID Connect tokens for integrating with 3rd party identity providers
- Webhook-based auth for delegating authentication to 3rd party services
- etc.

Multiple authentication modules can be enabled, and the first to match the request short-circuits the rest.  It is suggested to have at least two modules enables: the service account tokens authenticator, and one other user auth method.

Authorization is similar to authentication: different modules are supported, and the first module to reach an authorization decision about a request short-circuits the others.

There are 3 authorization modes:
1. [[Attribute-Based Access Control]]
2. [[Webhooks]]
3. [[Role-Based Access Control]]