Created on 2024-06-16_09-06-43

## 📔 Notes

### A note on CSRF
- attacker tricks user into performing an unauthorized action on an app. (transfer funds)
- user login (on a malicious login site)

### How to protect?

**state** variables:
- client app stores a unique state var in its session
- sent to authz server
- authz server sends back state var
- client verifies

### Example scenario of failed CSRF attack
- user logs in to client app with authz server flow (OIDC)
- client app generates a random state var for the session and is stored in the user's session storage
- attacker generates a farzi link with the wrong state
- client gets the redirect and finds out that the state var is different
    --> attack failed

## 🔗 Links

- [[Road to principal engineer]]