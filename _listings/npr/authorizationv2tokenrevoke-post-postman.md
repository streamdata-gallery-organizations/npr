{
  "info": {
    "name": "NPR Revoke an existing OAuth2 access token",
    "_postman_id": "8e578ba7-345f-4916-8d8e-ee26deb85dc8",
    "description": "Our implementation follows the proposed IETF specification [RFC-7009](https://tools.ietf.org/html/rfc7009).\n\nIf your client application offers the ability to for a logged-in user to log out, and you have access to a long-lived\n`client_credentials` token (i.e. you have generated one that you are storing securely for the lifetime of the entire app\ninstall), we suggest (but do not require) that you call this endpoint and revoke the access token belonging to the\nlogged-in user as part of your logout process. If you do not already have a long-lived `client_credentials` token,\nplease don't generate one just for the purposes of calling this endpoint.\n\nIf you are building a prototype application, we also recommend that you use this endpoint to clean up access tokens\nthat you generate during the testing of your app and do not intend to reuse.\n\nNote that revoking an access token will automatically revoke any refresh tokens associated with it, and vice-versa.",
    "schema": "https://schema.getpostman.com/json/collection/v2.0.0/"
  },
  "item": [
    {
      "name": "authorization",
      "item": [
        {
          "id": "6ac49bf7-a88a-4fe6-8632-e7a93f6895dc",
          "name": "revokeToken",
          "request": {
            "url": "http://api.npr.org/authorization/v2/token/revoke",
            "method": "POST",
            "header": [
              {
                "key": "Authorization",
                "value": "{}",
                "description": "A `client_credentials` access token from the same client application as the token being revoked",
                "disabled": false
              }
            ],
            "body": {
              "mode": "urlencoded",
              "urlencoded": [
                {
                  "key": "token",
                  "value": "{}",
                  "disabled": false,
                  "description": "The access token or refresh token that the client wants to have revoked"
                },
                {
                  "key": "token_type_hint",
                  "value": "{}",
                  "disabled": false,
                  "description": "A hint about the type of the token submitted for revocation"
                }
              ]
            },
            "description": "Our implementation follows the proposed IETF specification [RFC-7009](https://tools"
          },
          "response": [
            {
              "status": "OK",
              "code": 200,
              "name": "Response_200",
              "id": "1f86ea17-8dc1-47aa-8c32-57b28e20bbbe"
            }
          ]
        }
      ]
    }
  ]
}