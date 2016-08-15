=================================================
GET feedback/events.json
=================================================

Returns Feedback creation and response events that occur in a specified time period. Please note that the max to_time is 24 hours prior to the current time. For a more real­time response use webhooks or GET feedback/show/:id.json. E nhancements to this endpoint may be introduced in future releases.

Resource Infromation
----------------------------

+-------------------------------------------+------------------------------------------------+
| Response formats                          | JSON                                           |
+-------------------------------------------+------------------------------------------------+
| Requires authentication?                  | Yes (user context only)                        |
+-------------------------------------------+------------------------------------------------+
| Rate limited?                             | Yes                                            |
+-------------------------------------------+------------------------------------------------+
| Requests / 15 min window                  | 1,000                                          |
| (user auth)                               |                                                |
+-------------------------------------------+------------------------------------------------+

Parameters
----------------------------

+------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
| **from_time**          | Required on the 1st page. Epoch timestamp in milliseconds. Example: 1451936737470                                                                    |
| (required)             |                                                                                                                                                      |
|                        | The range is inclusive.                                                                                                                              |
+------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
| **to_time**            | Required on the 1st page. Epoch timestamp in milliseconds. Example: 1451936737470                                                                    |
| (required)             |                                                                                                                                                      |
|                        | The range is inclusive. The max to_time is 24 hours before current time. Requests for more recent data via this endpoint will receive an error.      |
+------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
| **count**              | Max number of results returned. Default and max is 100.         |                                                                                    |
| (required)             |                                                     |                                                                                                |
+------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
| **cursor**             | For paging through results. Required for paging through result sets greater than 1 page.                                                             |
| (optiona)              |                                                     |                                                                                                |
|                        | An empty value indicates you have reached the end of the result set.                                                                                 |
+------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+

Response Values
----------------------------

+------------------------+---------------------------------------------------------------------------+
| **events**             | An array of events.                                                       |
+------------------------+---------------------------------------------------------------------------+
| **event_type**         | Possible values: feedback.created, feedback.updated                       |
+------------------------+---------------------------------------------------------------------------+
| **next_cursor**        | Values are unique to a given from_time/to_time range.                     |
+------------------------+---------------------------------------------------------------------------+

Example Result
----------------------------

.. code:: javascript

	{
		"events":[
			{
				"event_type": "feedback.updated",
				"created_at": "SatDec1517:58:22+00002015",
				"feedback": {
					"created_at": "SatDec1517:58:20+00002015",
					"updated_at": "SatDec1517:59:22+00002015",
					"id": "123456789",
					...
				}
			},
			{
				"event_type": "feedback.created",
				"created_at": "SatDec1517:59:22+00002015",
				"feedback":{
					"created_at": "SatDec1517:59:22+00002015",
					"updated_at": "SatDec1517:59:22+00002015",
					"id": "123456799",
					...
				}
			}
		],
		"next_cursor": "10011"
	}