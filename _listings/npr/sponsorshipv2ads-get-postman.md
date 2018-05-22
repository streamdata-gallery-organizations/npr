{
  "info": {
    "name": "NPR Request DAAST sponsorship units",
    "_postman_id": "67b0e4b8-d775-403b-a203-15f4653ea49e",
    "description": "**Not** for use by NPR One clients (for whom sponsorship is already integrated into the Listening Service), this endpoint is designed to be used by our other client applications to request sponsorship on behalf of a user. Sponsorship units are returned in the form of DAAST XML. It is worth noting that this endpoint attempts to always return XML, even in the case of exceptions.\n\nThe default behavior of this endpoint is asynchronous; on an initial request, a call to our external sponsorship provider is placed on a queue, which is typically processed within 3 minutes. Once the sponsorship call is received and processed, the returned sponsorship units are placed in a cache on our server for the current user. Subsequent calls to this endpoint will return DAAST sponsorship units from this cache until tracking information is submitted, which removes the ad from the cache and will automatically request additional ads asynchronously if there are fewer than a certain number remaining in the cache.\n\nFor development purposes, it's worth noting that there is currently no way to clear a user's cache without submitting some form of tracking.",
    "schema": "https://schema.getpostman.com/json/collection/v2.0.0/"
  },
  "item": [
    {
      "name": "sponsorship",
      "item": [
        {
          "id": "9eabfd7a-fdeb-446a-b4f5-4aa7bd027fce",
          "name": "getAds",
          "request": {
            "url": "http://api.npr.org/sponsorship/v2/ads?adCount=%7B%7D&forceResult=%7B%7D&No Name=%7B%7D",
            "method": "GET",
            "body": {
              "mode": "raw"
            },
            "description": "**Not** for use by NPR One clients (for whom sponsorship is already integrated into the Listening Service), this endpoint is designed to be used by our other client applications to request sponsorship on behalf of a user"
          },
          "response": [
            {
              "status": "OK",
              "code": 200,
              "name": "Response_200",
              "id": "f547fa56-4acc-4ff0-9a88-0663a3b93409"
            }
          ]
        }
      ]
    }
  ]
}