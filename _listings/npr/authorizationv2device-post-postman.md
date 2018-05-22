{
  "info": {
    "name": "NPR Initiate an OAuth2 login flow for limited input devices",
    "_postman_id": "9310ad63-3b64-486e-98e2-fee7a3cf7836",
    "description": "This flow should only be used by clients who cannot show a native webview or do not have advanced input controls. It is an alternative to `GET /authorization/v2/authorize`.\n\nThird-party clients will need to use one or the other of these two endpoints, but they will generally not use both.",
    "schema": "https://schema.getpostman.com/json/collection/v2.0.0/"
  },
  "item": [
    {
      "name": "authorization",
      "item": [
        {
          "id": "c8ab11d0-9b72-4d06-b021-c04c526367c1",
          "name": "generateDeviceCode",
          "request": {
            "url": "http://api.npr.org/authorization/v2/device",
            "method": "POST",
            "body": {
              "mode": "urlencoded",
              "urlencoded": [
                {
                  "key": "client_id",
                  "value": "{}",
                  "disabled": false,
                  "description": "The client's ID"
                },
                {
                  "key": "client_secret",
                  "value": "{}",
                  "disabled": false,
                  "description": "The client's secret key"
                },
                {
                  "key": "scope",
                  "value": "{}",
                  "disabled": false,
                  "description": "A space-separated list of scope(s) requested by the application"
                }
              ]
            },
            "description": "This flow should only be used by clients who cannot show a native webview or do not have advanced input controls"
          },
          "response": [
            {
              "status": "OK",
              "code": 200,
              "name": "Response_200",
              "id": "13d9ec15-e5d8-4888-96a2-9f3c43d3b09f"
            }
          ]
        }
      ]
    }
  ]
}