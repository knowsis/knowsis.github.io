---
title: API Errors
last_updated: June 8, 2016
sidebar: api_sidebar
permalink: /api-errors/
---

## Errors

In the event of a problem with your request you will receive an error response

As much as possible, Knowsis attempts to use the appropriate HTTP status codes to indicate the general class of problem. We will also provide a body to the request in the requested format with more details on the problem where available. You should handle errors in your application and present your end users with a more friendly response than the error messages provided here.



<table>
  <thead><tr><th>Error Message</th><th>Description</th></tr></thead>
  <tbody>
    <tr><td>400 (Bad Request)</td><td>Any case where a parameter is invalid, or a required parameter is missing. This includes the case where OAuth parameters are not provided.</td></tr>
    <tr><td>401 (Unauthorized)</td><td>The OAuth signature was provided but was invalid.</td></tr>
    <tr><td>403 (Forbidden)</td><td>Access to the requested object was refused by the server. Your api account does not have permissions to access the request object.</td></tr>
    <tr><td>404 (Not Found)</td><td>The requested object does not exist.</td></tr>
    <tr><td>405 (Method Not Allowed)</td><td>Attempting to use POST with a GET-only endpoint, or vice-versa.</td></tr>
    <tr><td>409 (Conflict)</td><td>The request could not be completed as it is. Use the information included in the response to modify the request and retry.</td></tr>
    <tr><td>500 (Internal Server Error)</td><td>Our servers are having problems. The request is probably valid but needs to be retried later.</td></tr>
  </tbody>
</table>




Example error response body

```
{
  "error": {
    "errorCode": "400",
    "errorMessages": [
      "Missing parameter OAuth Consumer",
      "Missing parameter OAuth Nonce",
      "Missing parameter OAuth Signature"
    ]
  }
}
```

The error object is made up of the following fields:

<table>
  <thead><tr><th>Field</th><th>Type</th><th>Description</th></tr></thead>
  <tbody>
    <tr><td>errorCode</td><td>integer</td><td>The relevant HTTP error code</td></tr>
    <tr><td>errorMessages</td><td>list of strings</td><td>List of human readable error messages</td></tr>
  </tbody>
</table>


Additional details are provided in the errorMessages part of the error object. It should be one of the following types of errors.

<table>
  <thead><tr><th>Error Message</th><th>Description</th></tr></thead>
  <tbody>
    <tr><td>Missing OAuth parameter</td><td>The case where any of the required OAuth parameters are not provided. we will also specify the name of parameter that is missing.</td></tr>
    <tr><td>Invalid OAuth Consumer</td><td>The provided OAuth Consumer key was not valid</td></tr>
    <tr><td>Signature verification failed</td><td>The provided OAuth signature did not match that generated by the server.</td></tr>
    
  </tbody>
</table>
