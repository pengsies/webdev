# Fetching data

Javascript allows us to have dynamic content by fetching resources over the internet on demand.

Rather than fetching a new page from the server each time to show a different piece of information, we can choose to fetch a specific resource and update just update a small portion of the existing page instead.

Since we are choosing specific resources to fetch instead of a whole page, this greatly speeds up the user's ability to interact with the page.

## Request and response

The web is powered by the HTTP protocol.

Data is exchanged between clients and servers via HTTP messages.

In order for a client to fetch a piece of resource, it first needs to issue a **request** for it.

The server will then respond accordingly with a **response**, providing the data or telling the server why it can not serve the resource requested.

### Status codes

The server's response will always come with a status code, indicating how a resource was fetched or why it failed.

| Status Code | Meaning               | Description                                                                                               |
| ----------- | --------------------- | --------------------------------------------------------------------------------------------------------- |
| 200         | OK                    | The request was successful.                                                                               |
| 304         | Not Modified          | The requested resource has not been modified since the last request.                                      |
| 400         | Bad Request           | The server couldn't understand the request.                                                               |
| 401         | Unauthorized          | The request requires user authentication or lacks permission.                                             |
| 403         | Forbidden             | The server understood the request, but access is forbidden.                                               |
| 404         | Not Found             | The requested resource could not be found on the server.                                                  |
| 500         | Internal Server Error | An unexpected server error occurred.                                                                      |
| 502         | Bad Gateway           | The server, while acting as a gateway, received an invalid response from the upstream server it accessed. |
| 503         | Service Unavailable   | The server is currently unable to handle the request.                                                     |

Table generated by ChatGPT 2023-08-16

### Headers

TODO

### Body

TODO

## AJAX

Asynchronous JavaScript and XML

AJAX refers to an approach where a website uses **asynchronous** javascript to fetch resources using the `XMLHttpRequest` object.

### `XMLHttpRequest` object

```js
const httpRequest = new XMLHttpRequest();
```

The `XMLHttpRequest` object contains all the necessary methods to handle data fetching.

Before we send out our request, we need to decide what to do with the response we will receive.

To do this, we will need to supply another function which will run after the response has been received, also known as a callback function.

```js
function handler() {
  // Process the server response here.
  const resData = JSON.parse(httpRequest.responseText);
  console.log(resData);
}

httpRequest.onreadystatechange = handler;
```

Once the `onreadystatechange` method has been specified, we can proceed to issue our request.

```js
httpRequest.open(
  "GET",
  "https://api.data.gov.sg/v1/environment/2-hour-weather-forecast",
  true
);
httpRequest.send();
```

https://developer.mozilla.org/en-US/docs/Web/Guide/AJAX

## JSON

When viewing the headers for the response, it has the header `Content-Type: application/json`.

The body of the response is as follows:

```json
{
  "area_metadata": [
    {
      "name": "Ang Mo Kio",
      "label_location": { "latitude": 1.375, "longitude": 103.839 }
    }
  ],
  "api_info": { "status": "healthy" },
  "items": [
    {
      "update_timestamp": "2023-08-17T00:43:52+08:00",
      "timestamp": "2023-08-17T00:30:00+08:00",
      "valid_period": {
        "start": "2023-08-17T00:30:00+08:00",
        "end": "2023-08-17T02:30:00+08:00"
      },
      "forecasts": [
        { "area": "Ang Mo Kio", "forecast": "Partly Cloudy (Night)" }
      ]
    }
  ]
}
```

(do note that the rest of the regions other than Ang Mo Kio have been omitted for brevity)

TODO: explain how similar JSON and JS Objects are, how to convert them

The most common format of API responses is in JSON.

### XML

Another popular format to receive data is in XML, which is what the X in AJAX stands for.

```xml
<student>
  <name>
    Bob
  </name>
  <id>
    34120
  </id>
</student>
```

TODO: talk about similarity to HTML and declining popularity

## Fetch

The `fetch` API is a much more modern way to fetch data.

https://developer.mozilla.org/en-US/docs/Web/API/fetch

# Appendix

## Demonstration of requests and responses

Open the network tab and show them what a HTTP request and response looks like.

Need to remind students that not only 200 means success, 304 as well.

https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/304

Can demonstrate 304 by visiting a page and refreshing it.

## Demonstration on page load vs resource load

Open the network tab to show the size of a typical webpage, compared to the size of an API response.

Can take the chance to teach them about Round Trip Time (RTT).

## 2-hour Weather Forecast by NEA

https://api.data.gov.sg/v1/environment/2-hour-weather-forecast
https://beta.data.gov.sg/datasets/1456/view