# Google Maps Cost Problem

> An e-commerce platform allows users to search for nearby stores and delivery points based on their location. The platform relies heavily on the Google Maps API to provide accurate geolocation, route optimization, and distance calculations. However, due to the high frequency of API calls and large datasets, the platform faces high operational costs and latency issues. Developers need to optimize the use of the Google Maps API to reduce costs, minimize latency, and manage space complexity effectively.

After analysing the pricing structure and response of Google Maps API, I can see how the cost can be overwhelming in the long run when we have heavy traffic in the application.

Solutions: 
## Simple Solution (Caching): 
Places: We can use the *Places API* to get a whole list of our required topics in a area of 50000 KM (from the google docs). This data can be cached and refetched periodically for every area of hotspot locations to get all the stores we are interested in.
Routes: Since Google provides all the in between routes during a Compute Route API call. Example: (Part of response of the route API response)
```json
{"steps" : [
                        {
                            "distance" : {
                                "text" : "0,6 km",
                                "value" : 601
                            },
                            "duration" : {
                                "text" : "1 minute",
                                "value" : 77
                            },
                            "end_location" : {
                                "lat" : 51.5099409,
                                "lng" : -0.0870841
                            },
                            "html_instructions" : "Prendre la direction \u003cb\u003enord-est\u003c/b\u003e sur \u003cb\u003eBorough High St/A3\u003c/b\u003e vers \u003cb\u003eBedale St\u003c/b\u003e\u003cdiv style=\"font-size:0.9em\"\u003eContinuer de suivre A3\u003c/div\u003e\u003cdiv style=\"font-size:0.9em\"\u003eEntrée dans une section à péage\u003c/div\u003e",
                            "polyline" : {
                                "points" : "ypjyHxpPCG_@o@QY_AkAE?C?CCQSEGEEMQEEACGGIGeAo@]OA?ECQGGC_@KgHeBqAc@a@Iq@WYG_AUi@OIACAYG"
                            },
                            "start_location" : {
                                "lat" : 51.5049264,
                                "lng" : -0.0898856
                            },
                            "travel_mode" : "DRIVING"
                        },
                        {
                            "distance" : {
                                "text" : "0,2 km",
                                "value" : 152
                            },
                            "duration" : {
                                "text" : "1 minute",
                                "value" : 25
                            },
                            "end_location" : {
                                "lat" : 51.50989,
                                "lng" : -0.0883307
                            },
                            "html_instructions" : "Prendre légèrement \u003cb\u003eà gauche\u003c/b\u003e sur \u003cb\u003eArthur St\u003c/b\u003e",
                            "maneuver" : "turn-slight-left",
                            "polyline" : {
                                "points" : "cpkyHf_PGB_@EK?A?I@GFEHAJAJ?Z?V@NBRBPDVBFDHDLDFFFFFJFXL"
                            },
                            "start_location" : {
                                "lat" : 51.5099409,
                                "lng" : -0.0870841
                            },
                            "travel_mode" : "DRIVING"
                        },]
}
```
If we can cache the response for longer routes, then we can check if we already have the routes for the in between routes. 
Example: User wants to go from Koteshowr to Gatthaghar

 Case a) we dont have any cached data going from Koteshowr to Gatthaghar in any of the routes

 Case b) we have a cached route from Airport to Banepa, which includes Koteshowr to Gatthaghar in it


in case a) we have to fetch the route using google Maps API

in case b) we can just reuse specific portion of the route

> Note: But this is not allowed by google.

### [Google Policy Docs](https://developers.google.com/maps/documentation/route-optimization/policies#cache-policy)
### Pre-fetching, caching, or storage of content

Applications using the Route Optimization API are bound by the terms of your Agreement with Google. Subject to the terms of your Agreement, you must not pre-fetch, index, store, or cache any Content except under the limited conditions stated in the terms.

Note that the place ID, used to uniquely identify a place, is exempt from the caching restrictions. The place ID is returned in the `place_id` field in Route Optimization API responses. Learn how to save, refresh, and manage place IDs in the Place IDs guide.


## Most-cost-effective solution ?? :
**Host your own map server**: I really looked into this, since I found limited options to optimize the google maps API for cost cutting.. 

*WHY?*: The only thing I was sure of is that, using the google maps API in a very limited fashion (use free google embedding for the map, dont use any of the APIs until the user interacts with the map) can improve the cost performance on the site without caching any of the responses. Also, we can restrict our map to a specific location if we do this. Suppose our services are only available in Kathmandu valley, we can just add the maps of Kathmandu to our server. Also we can use the *Places API* to get a whole list of our required topics in a area of 50000 KM (from the google docs). This data can be cached and refetched periodically for every area of Kathmandu to get all the stores we are interested in.

*HOW?*: Since [PostGis](https://postgis.net/) is a open-source service, we can use this to store and maintain our own dataset of locations. I'm still not sure how everythingg will work but if we maintain our set of map service, it will be way more cost effective in the long run. I know it may take a lot of developer time but I really think this is the way to go if you really want a cost effective method.
