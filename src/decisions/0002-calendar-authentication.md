```
status: "draft"
date: 2023-10-03
```
# Calendar Authentication

## Context and Problem Statement


## Considered Options

Backend API endpoints auth methods:
* Basic Auth
* Sessions
* JWT

## Decision Outcome

Chosen option: "JWT" because it feels the most natural for a RESTful API, and doesn't need additional dependencies (e.g.: Redis for Sessions).

### Consequences

* Good, because it feels the most natural for a RESTful API
* Good, because it doesn't need any additional dependencies
* Good, because it can be easily enhanced with a third party authentication provider (e.g.: Google)
* Bad, because the already generated JWTs can't be invalidated

### Confirmation

PR code review

## Pros and Cons of the Options

### Basic Auth

* Good, because it is easy to implement on backend
* Good, because session management is not required
* Bad, because credentials need to be sent on every request

### Sessions

* Good, because it allows full control over the lifecycle of session
* Good, because it is more secure than Basic Auth. It is not required to send the credentials on every request
* Bad, because we need Redis to store sessions

### JWT

* Good, because it is more secure than Basic Auth. It is not required to send the credentials on every request
* Good, because we don't need Redis
* Good, because it can be easily enhanced with a third party authentication provider (e.g.: Google)
* Bad, because the already generated JWTs can't be invalidated

## More Information

{You might want to provide additional evidence/confidence for the decision outcome here and/or
 document the team agreement on the decision and/or
 define when/how this decision the decision should be realized and if/when it should be re-visited.
Links to other decisions and resources might appear here as well.}
