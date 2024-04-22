> Aim: remove lag between run terminating and lsrp and mapping being formed.


**Top-down**
```
./scripts/run
1) kms-qnl-service
2) key-routing-service // dive into this
```

Inspecting key-routing-service
```
KeyRouter.java
> lsrpRouter.start()
> startListening()
> > LSRPServerRouterInitializer
> > connectAdjacentNeighbours()
```

**Bottom-up**
- 
	- lsrp.log comes from `writeNetworkToFile`
	- mapping.log comes from `createMapping`
- both of them are referenced in:
	- onLSRP() -> LSRPIncomingClientHandler/channelRead -> 
	- checkLink() -> LinkDetectionRunnable
- LSRPIncomingClientHandler -> LSRPServerRouterInitializer
- LinkDetectionRunnable
	- onAdjacentNeighbourConnected 
		- > LSRPOutgoingClientHandler / channelActive.
		- > LSRPOutgoingClientInitializer 
	- checkLink // **doubt: recursion**
	- 
