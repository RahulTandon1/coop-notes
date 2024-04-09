> aim: figure out where the hex strings are generated in qkd-net

key comes from the QNLResponse payload received by ClientHandler.java's processResp.
It's used as an eventHandler in a Netty client in QNLKeyReader.

**What does the client send out?** 
Sends out a `request get alloc kp block`.

**What does it receive? How sends it this?**
Receives a QNLResponse
```
opId: RESP_GET_ALLOC_KP_BLOCK
  srcSiteId: B
  dstSiteId: A
  UUID: 8e18e113-573a-4bb8-b6d5-233b3d351f2b # blockID
```

API's newkey endpoint called
-> `keyPoolMgr.newKey(siteID);`
-> one of `fetchKey(sideID, null, -1L)`  or `new Key()` get returned.

**case `fetchKey(siteId, null, -1L)`**
all the locking aside, `key(poolName, index);` is returned.
- which calls `keyPools.get(poolName).getKey()`

---

### tracking all bootstraps
KMS
- Server in `kms-qnl-service`'s `KeyReceivingServer`
	- Port: `kms/qnl/config.yaml`
- Client in `kms-service` -> `QNLKeyReader`
	- ip: `kms-service/site.properties/qnl.port`
	- port: `kms-service/site.properties/qnl.port`

QNL
- Server in `key-routing-service` -> `KeyRouter`
	- Port: `qnl/config.yaml`
- Client in `key-routing-service` -> `KeyRouterConnectHandler`
	- For adj. sites:IP: adjSite.IP, port: adjSite.port / `qnl/config.yaml`
	- For KMS: local KMS's IP & POrt (qnl/config.yaml)
- Client & Server in `key-routing-service` -> `LSRPRouter`
- 

---

- [ ] Figure out where policy.check() code is actually injected.
- [ ] understand the requestparam syntax 
- [ ] fetchKey()
- [ ] new Key()
- [ ] @Value("${kms.site.id}") syntax. for localSiteId
- [ ] What is instanceID mentioned in `QNLConfiguration.java`?


---
What's the expected behaviour in terms of the config files?

```
.
├── kms
│   ├── kms.conf
│   ├── pools
│   │   └── B
│   │       └── A
│   │           └── d06c766d-6846-43f3-a079-1c72b241e435
│   ├── qnl
│   │   └── config.yaml
│   └── site.properties
├── kms.conf
├── mapping.log
├── qll-sim
│   └── qll-sim.conf
└── qnl
    ├── config.yaml
    ├── otp
    │   └── keys
    │       └── B
    │           └── otpkey
    ├── qll
    │   └── keys
    │       ├── B
    │       │   ├── B_0
    │       │   └── B_1
    │       └── C
    │           ├── C_0
    │           └── C_1
    └── routes.json
```