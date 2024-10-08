Created on 2024-06-15_07-53-02

## 📔 Notes

### OAuth2

#### Terminologies

1. Authz server: server that issues the access token, providing authz.
2. Resource server: server hosting the protected resource
4. Resource-owner: User --> granting permission to access resource.
3. Client: server making the request on behalf of the resource owner.
5. Access token: the token granted by authz server to access the resource on the resource server.
6. Refresh token: a token used to get a new access token without involving resource owner's permission.
7. Authz grant: creds required by authz server to provide access to resource server
    * authz code grant: obatined by authz code flow.
    * implicit: without authz code (less secure)
    * password: username:password from the user
    * client creds: get access token without resource owner involvement

#### Types

1. token endpoint: url to send authz code (or client creds in client_credentials grant type) to get access token
2. authz endpoint: the redirect url where we get permission from the resource owner
3. redirect url: url to redirect to after the authz is granted by the resource owner
4. scope: the permission the client is asking from the resource owner

### OIDC

1. Identity provider (IDP): authz server in oauth. (provides ID token as well)
2. Relying party (RP): the server that obtains the user info from the IDP (client in oauth)
3. ID token: JWT that contains user info (aka claims)
4. claims: user info (name, email, etc)

**Oauth2.0:** --> primarily for authorization (limited temp access to resources)
**OIDC:** --> extend oauth to get identity of the user from the authz server

## 🔗 Links

- [[Road to principal engineer]]
- [[Tech]]
