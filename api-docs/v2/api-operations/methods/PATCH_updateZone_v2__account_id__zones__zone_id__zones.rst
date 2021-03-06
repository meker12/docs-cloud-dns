.. _PATCH_updateZone_v2__account_id__zones__zone_id__zones:

Update a zone
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    PATCH /v2/{TENANT_ID}/zones/{zoneId}

This operation modifies DNS zone attributes only. Records cannot be added, modified, or 
deleted. Only the TTL, email address and description attributes of a zone can be modified.

..  note:: 

    - This operation returns an asynchronous response. For information about how
      asynchronous operations work, see 
      :ref:`Synchronous and asynchronous responses<cdns-dg-synch-asynch>`.  

If the corresponding request cannot be fulfilled because of insufficient or invalid data, 
an ``HTTP 400`` (Bad Request) error response is returned with information about the 
failure in the body of the response. Failures in the validation process are 
non-recoverable and require you to correct the cause of the failure and resend the request.

..  note:: 

    -  After a DNS change is made, it might take up to a minute for the change to propagate 
       to Rackspace name servers. For information about DNS propagation, see 
       :ref:`DNS propagation<cdns-dg-propagation>`.

This table shows the possible response codes for this operation:

+---------+-----------------------+---------------------------------------------+
| Response| Name                  | Description                                 |
| code    |                       |                                             |
+=========+=======================+=============================================+
| 200     | Success               | The request succeeded.                      |
+---------+-----------------------+---------------------------------------------+
| 201     | Created               | The request was fulfilled and a new resource|
|         |                       | was created.                                |
+---------+-----------------------+---------------------------------------------+
| 400     | Bad Request           | The request is missing one or more          |
|         |                       | elements, or the values of some elements    |
|         |                       | are invalid.                                |
+---------+-----------------------+---------------------------------------------+
| 401     | Unauthorized          | You are not authorized to complete this     |
|         |                       | operation. This error can occur if the      |
|         |                       | request is submitted with an invalid        |
|         |                       | authentication token.                       |
+---------+-----------------------+---------------------------------------------+
| 403     | Forbidden             | The server did not find anything matching   |
|         |                       | the request URI.                            |
+---------+-----------------------+---------------------------------------------+
| 404     | Not Found             | The requested item was not found.           |
+---------+-----------------------+---------------------------------------------+
| 405     | Method Not Allowed    | The method specified in the request is      |
|         |                       | not allowed for the resource identified by  |
|         |                       | the request URI.                            |
+---------+-----------------------+---------------------------------------------+
| 409     | Already Exists        | The item already exists.                    |
+---------+-----------------------+---------------------------------------------+
| 413     | Over Limit            | The request exceeds the rate limit or quota.|
+---------+-----------------------+---------------------------------------------+
| 415     | Unsupported Media     | The server won't service the                |
|         | Type                  | request because the entity of the request   |
|         |                       | is in a format not supported by the         |
|         |                       | requested resource for the requested        |
|         |                       | method.                                     |
+---------+-----------------------+---------------------------------------------+
| 503     | Service Unavailable   | The service is not available.               |
+---------+-----------------------+---------------------------------------------+

Request
""""""""""""""""

This table shows the URI parameters for the request:

+-----------------------+---------+---------------------------------------------+
| Name                  | Type    | Description                                 |
+=======================+=========+=============================================+
| ``{TENANT_ID}``       | ​String | The account ID of the account owner.        |
+-----------------------+---------+---------------------------------------------+
| ``{zoneId}``          | ​String | The ID of the zone to be updated.           |
+-----------------------+---------+---------------------------------------------+

The following table shows the body parameters for the request:

+-----------------------+------------+---------------------------------------------+
| Name                  | Type       | Description                                 |
+=======================+============+=============================================+
| **name**              | ​String    | The name for the zone, which cannot be      |
|                       |            | changed. Must be a valid zone (domain) name.|
+-----------------------+------------+---------------------------------------------+
| **email**             | ​String    | Email address to use for contacting the zone|
|                       |            | administrator.                              |
+-----------------------+------------+---------------------------------------------+
| **ttl**               | Integer    | Time-to-live numeric value in seconds. The  |
|                       | (Optional) | default (and minimum) value is 300 seconds. |
+-----------------------+------------+---------------------------------------------+
| **description**       | ​String    | A description of the zone.                  |
|                       | (Optional) |                                             |
+-----------------------+------------+---------------------------------------------+
| **masters**           | ​Object    | An array of master name servers. (NULL for  |
|                       | (Optional) | type PRIMARY, required for SECONDARY        |
|                       |            | otherwise the zone will not be transfered   |
|                       |            | before set.                                 |
+-----------------------+------------+---------------------------------------------+
 
**Example: Update a zone, request**

.. code::  

    PATCH /v2/123456/zones/a86dba58-0043-4cc6-a1bb-69d5e86f3ca3 HTTP/1.1
    Host: global.dns.rackspacecloud.com
    Accept: application/json
    Content-Type: application/json

    {
        "ttl": 3600
    }

Response
""""""""""""""""

This table shows the body parameters for the response:

+--------------------------------+----------------------+----------------------+
|Name                            |Type                  |Description           |
+================================+======================+======================+
|**id**                          |Uuid                  |The ID of the zone.   |
+--------------------------------+----------------------+----------------------+
|**pool_id**                     |Uuid                  |The ID of the pool.   |
+--------------------------------+----------------------+----------------------+
|**project_id**                  |Integer               |The project, account, |
|                                |                      |or tenant ID.         |
+--------------------------------+----------------------+----------------------+
|**name**                        |String                |The name of the zone. |
+--------------------------------+----------------------+----------------------+
|**email**                       |String                |The email of the      |
|                                |                      |zone's owner.         |
+--------------------------------+----------------------+----------------------+
|**ttl**                         |Integer               |The time to live for  |
|                                |                      |the zone.             |
+--------------------------------+----------------------+----------------------+
|**serial**                      |Uuid                  |The epoch time stamp  |
|                                |                      |indicating the        |
|                                |                      |creation date of the  |
|                                |                      |zone or the latest    |
|                                |                      |update date.          |
+--------------------------------+----------------------+----------------------+
|**status**                      |String                |The status of the     |
|                                |                      |zone.                 |
+--------------------------------+----------------------+----------------------+
|**description**                 |Uuid                  |The description       |
|                                |                      |of the zone.          |
+--------------------------------+----------------------+----------------------+
|**masters**                     |Array                 |An array of master    |
|                                |                      |nameservers.          |
+--------------------------------+----------------------+----------------------+
|**type**                        |String                |The type of zone.     |
|                                |                      |The values are either |
|                                |                      |``PRIMARY`` or        |
|                                |                      |``SECONDARY``.        |
+--------------------------------+----------------------+----------------------+
|**version**                     |Integer               |The version of the    |
|                                |                      |zone export.          |
+--------------------------------+----------------------+----------------------+
|**transferred_at**              |Datestamp             |The time stamp        |
|                                |                      |indicating the        |
|                                |                      |transfer date of the  |
|                                |                      |zone export.          |
+--------------------------------+----------------------+----------------------+
|**created_at**                  |Datestamp             |The time stamp        |
|                                |                      |indicating the        |
|                                |                      |creation date of the  |
|                                |                      |zone export.          |
+--------------------------------+----------------------+----------------------+
|**updated_at**                  |Datestamp             |The time stamp        |
|                                |                      |indicating the date   |
|                                |                      |that the zone export  |
|                                |                      |was last updated.     |
+--------------------------------+----------------------+----------------------+
|**links**                       |Object                |A container with the  |
|                                |                      |links to the exports. |
+--------------------------------+----------------------+----------------------+
|links.\ **self**                |Uuid                  |The link to the       |
|                                |                      |zone exports (self).  |
+--------------------------------+----------------------+----------------------+

**Example:  Update a zone, response**

.. code::  

    HTTP/1.1 200 OK
    Content-Type: application/json

    {
        "id": "a86dba58-0043-4cc6-a1bb-69d5e86f3ca3",
        "pool_id": "572ba08c-d929-4c70-8e42-03824bb24ca2",
        "project_id": "123456",
        "name": "example.org.",
        "email": "joe@example.org.",
        "ttl": 3600,
        "serial": 1404760160,
        "status": "ACTIVE",
        "description": "This is an example zone.",
        "masters": [],
        "type": "PRIMARY",
        "transferred_at": null,
        "version": 1,
        "created_at": "2014-07-07T18:25:31.275934",
        "updated_at": "2014-07-07T19:09:20.876366",
        "links": {
          "self": "https://global.dns.api.rackspacecloud.com/v2/123456/zones/a86dba58-0043-4cc6-a1bb-69d5e86f3ca3"
        }
    }
