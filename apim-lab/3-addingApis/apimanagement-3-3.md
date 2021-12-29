---
title: Calling Apis
parent: Adding API's
has_children: false
nav_order: 3
---



### Calling API and testing Subscription Keys


Let's add another API, the [Color API](https://markcolorapi.azurewebsites.net/swagger/).

![](../../assets/images/APIMColorAPI.png)

- Create a new API with OpenAPI specification and import swagger from <https://markcolorapi.azurewebsites.net/swagger/v1/swagger.json>
  - Use the API URL suffix **color**.

![](../../assets/images/APIMAddColorAPI1.png)

![](../../assets/images/APIMAddColorAPI2.png)

We can test the newly-added API from the *Test* tab. Note the successful **200** response.

![](../../assets/images/APIMAddColorAPI.png)

- Products can be configured after the API is initially created as well. On the *Settings* tab, set *Products* to include `Starter` and `Unlimited`, then press *Save*.

![](../../assets/images/APIMAddColorAPIProducts.png)

- Switch to the Developer portal and look at the *Color* API.
  - Try the *ApiRandomColorGet* operation.
- Notice the successful `200` response and the returned random color.

![](../../assets/images/APIMColorTryIt1.png)

![](../../assets/images/APIMColorTryIt2.png)

### Rate limit

API management uses rate limiting to protect APIs from being overwhelmed and helps prevent exposure to DDoS attacks. As APIM sits in between your API and their callers, it effectively governs access to your APIs.  

We are going to use the [Color](https://markcolorweb.azurewebsites.net) website to demonstrate how rate limiting is applied. The website displays 500 lights. Each light will randomly make a call to the RandomColor API and then apply the returned color to the lights.

![](../../assets/images/APIMColorWeb.png)

First, we need to enable CORS for the domain name of the frontend. To achieve this we have to do the following in APIM:

- On the sidemenu, click on `APIs`, then select the `All APIs` option.
- Inside the `Inbound processing` area you will see the `cors` policy, which we added in part 2 by pressing the `Enable Cors` button.
- Click on the pencil icon next to that policy to edit it.

![](../../assets/images/apim-policy-cors-all-apis.png)  

- Here we will see this form where we can add the domain name of our frontend `https://markcolorweb.azurewebsites.net` or the `*` for all domains. Press *Add allowed origin*, enter the URL, then press *Save*.

![](../../assets/images/apim-policy-cors-all-apis2.png)

- After enabling CORS in APIM lets go back to our frontend <https://markcolorweb.azurewebsites.net> and follow these steps:

- Click on the hamburger menu next to *Colors* in the top left corner.
- Click on *Config*.
- Replace the *API URL* according to this format:
  - <https://YOURAPIM.azure-api.net/color/api/randomcolor>
- After setting the API URL correctly, press the hamburger menu again and go to *Home*. 
- Press *Start* to see how the frontend is calling the api. You should see a *401* response, indicating an auth error.
  - Our API requires a subscription, but we have not yet entered a subscription key. 

![](../../assets/images/APIMColorWebConfig401.png)

- The subscription keys can be fetched from the Developer Portal. Open the main Developer Portal page, then click on *Profile* in the top menu. 
- Copy the following URL into Notepad, modify your APIM instance, then copy the URL, so that you have two of the same URLs. We will use them for the *Starter* and *Unlimited* pathways into APIM.
  - `https://YOURAPIM.azure-api.net/color/api/RandomColor?key=`
- Append the primary keys for both subscriptions - one key per URL - to get unique URLs for *Starter* and *Unlimited*.
  
![](../../assets/images/APIMColorWebKeys.png)

- To see that *Unlimited* product has no rate limits:
  - Configure the Color website to use the Unlimited URL.
  - Select [Start].
  - Notice there is no rate limit - every light is randomly and continuously updated. 

![](../../assets/images/APIMColorWebUnlimited.png)

- To see that *Starter* product is limited to 5 calls per minute:
  - Configure the Color website to use the Starter URL.
  - Select [Start].
  - Notice that only 5 lights get colored.

![](../../assets/images/APIMColorWebStarter.png)

- Try the same *Starter* URL directly in your web browser:
  - Notice the error status / message returned.
    - Example: *{ "statusCode": 429, "message": "Rate limit is exceeded. Try again in 40 seconds." }*

![](../../assets/images/APIMColorWebStarterbrowser.png)

