# PnP Sites Core Library - Modified to Retrieve and Install App Catalog Apps via On-Premise SharePoint Solutions

A slight modification to this library to get App Catalogs Apps retrieved and installed via AppManager.Install() and AppManager.GetAvailable().

I was receiving the following error when using this library: **Dynamic Operations Can Only Be Performed In Homogenous AppDomain**

The line causing the error:
request.Headers.Add("X-RequestDigest", await **context.GetRequestDigestAsync()**);

For some reason, old ClientContext code is being used here to retrieve the Request Digest value via a web request. I wrote a new function (GetRequestDigest()) to retrieve the request digest using a ClientContext object with Site Collection Admin-level credentials attached (can't be the Farm Admin account - I suggest using SecureStore to retrieve credentials). The request is very similar to the other REST requests inside the AppManager class.
