# Dynatrace npm module for PaaS

This module adds enterprise grade monitoring for Node.js in PaaS environments that aren't supported by a dedicated integration.
Before using this module, please [review the Dynatrace documentation](https://www.dynatrace.com/support/help/cloud-platforms/) to
make sure that there isn't already a marketplace integration or buildpack available for your platform.

## Installation

* [Sign up for free](https://www.dynatrace.com/trial/) and follow the instructions
* Click on "Deploy Dynatrace"
* Click on "Set up PaaS Integration"
* Generate a PaaS token
* Run `$ npm install git + https://github.com/EricMaillard/agent-nodejs.git` in your project directory
* Run that API request to get tenantUUID, tenantToken and communicationEndpoints:
* For Dynatrace Managed:
     curl -X GET https://{your-domain}/e/{your-environment-id}/api/v1/deployment/installer/agent/connectioninfo -H "accept: application/json" -H "Authorization: Api-Token pass_token"
* For Dynatrace SaaS:
     curl -X GET https://{your-environment-id}.live.dynatrace.com/api/v1/deployment/installer/agent/connectioninfo -H "accept: application/json" -H "Authorization: Api-Token pass_token"
* This request will return that paylaod:
*    "tenantUUID" : "<tenant uuid>",
*    "tenantToken" : "<tenant token>"
*    "communicationEndpoints" : [ <endpoint1>, <endpoint2>, <endpoint3> ]

* Using the returned data add the following code block as first statement to your application

```js
try {
  require('@dynatrace/oneagent')({
    tenantUUID : "<tenant uuid>",
    tenantToken : "<tenant token>",
    communicationEndpoints : "<communication endpoint, for instance url of an ActiveGate>"
  });
} catch (err) {
  console.log('Failed to load OneAgent: ', err);
}
```

### Emitting debug output

To enable debug output set the `DEBUG` environment variable to `dynatrace*`. For more detail see the [debug module documentation](https://www.npmjs.com/package/debug).

## Licence

Licensed under the MIT License. See the LICENSE file for details.
