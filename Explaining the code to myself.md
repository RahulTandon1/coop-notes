# 1: Networking aspects to myself

# 2 : Phrase problem in networking terms


----


#### What do `scripts/run` do?
- makes `qkd_logs` dir
- export an env var called `SITE_PROPERTIES` (path to .qkd/kms/site.properties)
- starts 8 services using the terminal multiplexer `screen`
	1. registration
	2. KMS API gateway
	3. KMS service
	4. config service
	5. qll simulation
	6. kms-qnl
	7. key-routing
	8. auth-service
runs things under the hood using `java -jar <path to jar>`





---

# Key Flow document

Step 4
- Mentioned `REQ_GET_ALLOC_KP_BLOCK`(defined in QNLConstants.java). This is used in 3 places. Question: *which of the 3 gets triggered in Step 4?*
	- ClientHandler.java
	- KeyRouterFrontendHandler's  `processReq` (called in `channelRead`)
	- QNLRequest.java methods -> encode, decode, opIdToString
I think ClientHandler.java's channelActive gets triggered.
But, based on a response by Perplexity, I think `channelActive` is run independent of this. It might get triggered the moment **some** channel connection gets constructed.


Step 5
The KeyRouterFrontendHandler receives the request. Since the file is located in key-routing-service, it checks out with the point's details. 
In `processReq`, we create a new QNLRequest.

At the end we trigger the next (in the ChannelPipeline) ChannelInboundHandler's channelActive and channelRead methods


> DOUBT: What does our ChannelPipelineConsist of?

> DOUBT: Does `KeyRouterFrontendHandler`'s channelRead recurse on itself?



Step 6
No we're back in KeyRouterFrontendHandler.java, but a different case `REQ_GET_KP_BLOCK_INDEX`. We fire another event `REQ_POST_ALLOC_KP_BLOCK`. 
> DOUBT: Not sure how this goes to the KMS-QNL service


> DOUBT: Why are some log.info's not showing up in VS code search: `LOGGER.info("REQ_GET_KP_BLOCK_INDEX/generate new QNLRequest:" + req);`

> DOUBT: The handler for `REQ_POST_ALLOC_KP_BLOCK` is in ServerHandler.java. Not sure how the 2 files  (KeyRouterFrontendHandler.java and this ServerHandler.java) communicate with each other?


Step 7:
There's just one case in the processReq of kms-qnl-service's ServerHandler.java which uses QNLUtils.writekeys to write things to the filesystem. It fires a QNLResponse with opID `RESP_POST_ALLOC_KP_BLOCK`

Step 8: The handler for that opID lives in key-routing-service's KeyRouterBackendHandler.java 
It fires a QNLResponse with the respOpID from the request. This was set in ServerHandler.java's `REQ_POST_ALLOC_KP_BLOCK` which also delegated it to its qReq.getRespOpId. KeyRouterFrontendHandler.java's processReq's `REQ_GET_KP_BLOCK_INDEX` case had set the respOpId to `RESP_GET_KP_BLOCK_INDEX`

Step 8:
The handler for RESP_GET_KP_BLOCK_INDEX lives key-routing-service's `KeyRouterBackendHandler`. It reads from the QLL layer and sends a QNLResponse with an opID of  `RESP_GET_ALLOC_KP_BLOCK. 

I do not get where the handler for `RESP_GET_KP_BLOCK_INDEX` is andhow it relates to the KMS-service layer.

