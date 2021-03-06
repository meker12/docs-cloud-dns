.. _get-show-limits-v1.0-account-limits-type:

Show limits
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /v1.0/{account}/limits/{type}

Shows assigned limits for a specified type.

This call provides a list of all applicable limits of a specified ``type`` for the specified 
account.

The following examples show the requests and corresponding responses to list all applicable 
limits of a specified ``type`` for the specified account.


This table shows the possible response codes for this operation:

+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |Success                  |Request succeeded.       |
+--------------------------+-------------------------+-------------------------+
|400 500                   |dnsFault                 |The DNS service has      |
|                          |                         |experienced a fault.     |
+--------------------------+-------------------------+-------------------------+
|401                       |Unauthorized             |You are not authorized   |
|                          |                         |to complete this         |
|                          |                         |operation. This error    |
|                          |                         |can occur if the request |
|                          |                         |is submitted with an     |
|                          |                         |invalid authentication   |
|                          |                         |token.                   |
+--------------------------+-------------------------+-------------------------+
|503                       |Service Unavailable      |The service is not       |
|                          |                         |available.               |
+--------------------------+-------------------------+-------------------------+

Request
""""""""""""""""

This table shows the header parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|X-Auth-Token              |String                   |Arbitrary character      |
|                          |                         |string generated by the  |
|                          |                         |authentication service   |
|                          |                         |in response to valid     |
|                          |                         |credentials.             |
+--------------------------+-------------------------+-------------------------+

This table shows the URI parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|{account}                 |String                   |The tenant ID.           |
+--------------------------+-------------------------+-------------------------+
|{type}                    |String                   |The type of limit.       |
+--------------------------+-------------------------+-------------------------+

This operation does not accept a request body.

**Example List Specified Limit: XML request**


.. code::

   GET https://dns.api.rackspacecloud.com/v1.0/1234/limits/rate_limit
   Accept: application/xml
   X-Auth-Token:
   									ea85e6ac-baff-4a6c-bf43-848020ea3812
   Content-Type: application/xml
   Content-Length: 0
   
**Example List Specified Limit: JSON request**

.. code::

   GET https://dns.api.rackspacecloud.com/v1.0/1234/limits/rate_limit
   Accept: application/json
   X-Auth-Token:
   									ea85e6ac-baff-4a6c-bf43-848020ea3812
   Content-Type: application/json
   Content-Length: 0

Response
""""""""""""""""

**Example List Specified Limit: XML response**

.. code::

   Status: 200 OK
   Date: Thu, 28 Jul 2011 21:54:21 GMT
   X-API-VERSION:
   									1.0.17
   Content-Type: application/xml
   Content-Length: 678
   
   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <limits xmlns="http://docs.openstack.org/common/api/v1.0">
       <rates>
           <rate uri="*/status/*" regex=".*/v\d+\.\d+/(\d+/status).*">
               <limit verb="GET" value="5" remaining="0" unit="SECOND"/>
           </rate>
           <rate uri="*/domains*" regex=".*/v\d+\.\d+/(\d+/domains).*">
               <limit verb="GET" value="100" remaining="0" unit="MINUTE"/>
               <limit verb="POST" value="25" remaining="0" unit="MINUTE"/>
               <limit verb="PUT" value="50" remaining="0" unit="MINUTE"/>
               <limit verb="DELETE" value="50" remaining="0" unit="MINUTE"/>
           </rate>
       </rates>
   </limits>
   
**Example List Specified Limit: JSON response**

.. code::

   Status: 200 OK
   Date: Thu, 28 Jul 2011 21:54:21 GMT
   X-API-VERSION:
   									1.0.17
   Content-Type: application/json
   Content-Length: 671
   
   {
     "rates" : {
       "rate" : [ {
         "uri" : "*/status/*",
         "limit" : [ {
           "value" : 5,
           "verb" : "GET",
           "unit" : "SECOND"
         } ],
         "regex" : ".*/v\\d+\\.\\d+/(\\d+/status).*"
       }, {
         "uri" : "*/domains*",
         "limit" : [ {
           "value" : 100,
           "verb" : "GET",
           "unit" : "MINUTE"
         }, {
           "value" : 25,
           "verb" : "POST",
           "unit" : "MINUTE"
         }, {
           "value" : 50,
           "verb" : "PUT",
           "unit" : "MINUTE"
         }, {
           "value" : 50,
           "verb" : "DELETE",
           "unit" : "MINUTE"
         } ],
         "regex" : ".*/v\\d+\\.\\d+/(\\d+/domains).*"
       } ]
     }
   }




