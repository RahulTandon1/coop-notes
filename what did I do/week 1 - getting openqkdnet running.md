delete any remnants of previous stuff:
rm -rf the following:
```
~/config-repo/
~/.qkd
~/qkd_logs
```

We run OpenQKDNet and got alice and bob working. The end result looked something like this:

![[media/Screenshot from 2024-02-09 16-26-50.png]]

**Reflecting on what this means**
- So we got 2 nodes to "talk to each other".
- We got a file transferred between these nodes "somehow"
- Not sure how though.
- There's something related to an SSL/TLS PSK Hint. No clue what that means. I think it's something related to fast session-restart.