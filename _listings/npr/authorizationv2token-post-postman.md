{
  "info": {
    "name": "NPR Create a new OAuth2 access token",
    "_postman_id": "438f232b-f6ff-4c52-9cdc-bf023aff30a4",
    "description": "Please be aware that the required parameters are contingent on the `grant_type` that you select.\n\nFor the `authorization_code` grant type, you are **required** to pass in the `code` and `redirect_uri` parameters. `service`, `username` and `password` parameters will be ignored.\n\nFor the `client_credentials` grant type, you do not need to pass in any additional parameters beyond the basic requirements. `code`, `redirect_uri`, `service`, `username` and `password` parameters will be ignored.\n\nFor the `device_code` grant type, you are **required** to pass in the `code` parameter. `redirect_uri`, `service`, `username` and `password` parameters will be ignored.\n\nFor the `password` grant type, you are **required** to pass in the `username` and `password` parameters. If you are logging in via a social service, you should also pass in the `service` parameter. (In this case, the access token you receive from the social service will serve as both your username and password.) The `code` and `redirect_uri` parameters are ignored.\nThird-party developers do not have access to this grant type.\n\nFor the `refresh_token` grant type, you are **required** to pass in the `refresh_token` parameter. The `scope` parameter can optionally be used to request a different set of scopes than were used in the original request, but it **cannot** contain any scopes that were not previously requested. If not specified, then `scope` will be set to whichever scopes were used for the original access token request. If trading in an old non-expiring access token for a refresh-enabled token, set the value of `refresh_token` to the access token value and `token_type_hint` must be set to `access_token`. `code`, `redirect_uri`, `service`, `username` and `password` parameters will be ignored.\n\nThe `temporary_user` and `anonymous_user` grant types are custom grant types created by NPR to suit our needs for functionality such as our &quot;try-before-you-buy&quot; experience. If you are a third-party developer, you will not have access to these grant types unless we have explicitly given you permission within our system.\nFor these grant types, you do not need to pass in any additional parameters beyond the basic requirements. `code`, `redirect_uri`, `service`, `username` and `password` parameters will be ignored.\n\nIf you are unsure of which grant type to select, assume that `authorization_code` is the one you want.\n\nNote that at this time, refresh tokens are an opt-in feature; however, in the future, they will gradually transition to being opt-out, and ultimately required for all clients. Our general guidance at this time is that if this endpoint starts returning refresh tokens for you, you are responsible for implementing the code to handle them appropriately in accordance with the OAuth 2.0 spec. For more information about our gradual rollout of this feature, please contact the NPR One API team.",
    "schema": "https://schema.getpostman.com/json/collection/v2.0.0/"
  },
  "item": [
    {
      "name": "authorization",
      "item": [
        {
          "id": "82ef5772-427f-4717-94b8-cd923d0f30aa",
          "name": "createToken",
          "request": {
            "url": "http://api.npr.org/authorization/v2/token",
            "method": "POST",
            "body": {
              "mode": "urlencoded",
              "urlencoded": [
                {
                  "key": "client_id",
                  "value": "{}",
                  "disabled": false,
                  "description": "The client's ID, required for all grant types"
                },
                {
                  "key": "client_secret",
                  "value": "{}",
                  "disabled": false,
                  "description": "The client's secret, required for all grant types"
                },
                {
                  "key": "code",
                  "value": "{}",
                  "disabled": false,
                  "description": "Required for `authorization_code` and `device_code` grant types"
                },
                {
                  "key": "grant_type",
                  "value": "{}",
                  "disabled": false,
                  "description": "The type of grant the client is requesting"
                },
                {
                  "key": "password",
                  "value": "{}",
                  "disabled": false,
                  "description": "Required for `password` grant type"
                },
                {
                  "key": "redirect_uri",
                  "value": "{}",
                  "disabled": false,
                  "description": "Required for `authorization_code` grant type"
                },
                {
                  "key": "refresh_token",
                  "value": "{}",
                  "disabled": false,
                  "description": "Required for `refresh_token` grant type"
                },
                {
                  "key": "scope",
                  "value": "{}",
                  "disabled": false,
                  "description": "Optionally used by the `refresh_token` grant type only"
                },
                {
                  "key": "service",
                  "value": "{}",
                  "disabled": false,
                  "description": "If logging in via a social service, this parameter should be set"
                },
                {
                  "key": "token_type_hint",
                  "value": "{}",
                  "disabled": false,
                  "description": "A hint about the type of the token submitted for a new access and refresh token"
                },
                {
                  "key": "username",
                  "value": "{}",
                  "disabled": false,
                  "description": "Required for `password` grant type"
                }
              ]
            },
            "description": "Please be aware that the required parameters are contingent on the `grant_type` that you select"
          },
          "response": [
            {
              "status": "OK",
              "code": 200,
              "name": "Response_200",
              "id": "0d6c5dcc-ff04-4591-95ba-22a49c5f6a65"
            }
          ]
        }
      ]
    }
  ]
}