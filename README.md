Usage Instructions:
- run python burp_parser.py to initiate the test
python burp_parser.py --requests request_file_or_folder --model coral_model.json --service serviceName

requests is mandatory, and refers to a folder containing burp request files (right click on a Burp request or highlight a bunch of requests in the Proxy History tab, and click "Save Item". All the highlighted (or single) request will get saved to a single request file) or a burp request file directly

model parameter is used to specify the Coral model associated with the particular service that the Burp requests belong to. This is done to determine the Action/API name of the request (ie. ListUsers, GetCallerIdentity, ListTables, etc.). If the request contains the x-amz-target header, then the model parameter is not required. The API endpoint name could also be specified in the actual request itself, through the use of the ActionName header.

The ServiceName parameter can be provided to override the default service name extracted from the requests, although this is probably not going to be used very often (FEATURE NOT YET IMPLEMENTED)

Important:
- if the request contains the x-amzn-target header, then a model file is not required

Caveats:
- One assumption that the code makes is that all the requests belong to the same service. Errors in the result may occur if requests from different services are used in the same testcase.
- temporary credentials cannot be used. CLI must have a default AWS profile configured 
- service calls requiring a custom signed headers such as s3api listbuckets, which requires the x-amzn-hash-sha256

TEST COMMAND:
python burp_parser.py --request bughunt_requests --model bughunt_model.json --service bugbust