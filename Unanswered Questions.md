- What's Ninja?
- What's a dynamically linked library.
- How does the CA know I own a certain domain name?

- **Application Data section of the Module 6 of Practical TLS**

What I think we said:
Record =
```
header
---
Payload
HMAC of header + payload
padding
```
- AEAD does the following:
	- integrity on both Header + Payload (application data).
	- encryption on application data

Question:
- why do we need that padding?
- if we do an HMAC, then isn't the length inaccurate? Was this why we had to add the padding?
- how does AEAD get the record length right?
- How does AEAD work


- What are git submodules (in context of oqsprovider in openssl git repo)
- What is a Hilbert space?
- What is a metric space?


**Networking**
- Motivating example for routers: 2 different classroom with different requirements (internet + cloud resources vs just internet). In a real scenario, I would do this in an application layer thing right? (Who can access what), or would it be a problem to solve earlier on in the stack (used very loosely here)? For example: I could either have GSuite or something which lets me decide what all can be accessed based on account ID, or I could say hosts with `192.168.1.x` can access certain things, but others cannot. 
	- We'd only implement one of the two right?
	- For something more generalized than my local network, I would expect this to be in the application layer.
- Who assigns a router an IP address?
- Does the switch have an IP address? Can nodes tell whether they're connected to a router via a switch, or they cannot?
- how does tcpdump perform ip address -> name mapping? Sounds like a reverse DNS lookup.
- Should an application/program be able to choose a scheduler? Are there any guarantees one can get about a scheduler?

```
public static void show() {  
  
    Map<Integer, String> numbers = new ConcurrentHashMap<>();  
    var thread1 = new Thread(() -> {  
        numbers.put(1, "A");  
        numbers.put(2, "A");  
        numbers.put(3, "A");  
        numbers.put(4, "A");  
        numbers.put(5, "A");  
        numbers.put(6, "A");  
    });  
  
    var thread2 = new Thread(() -> {  
        numbers.put(1, "B");  
        numbers.put(2, "B");  
        numbers.put(3, "B");  
        numbers.put(4, "B");  
        numbers.put(5, "B");  
        numbers.put(7, "B");  
    });  
  
    thread1.start();  
    thread2.start();  
  
    try {  
        thread1.join();  
        thread2.join();  
    } catch (InterruptedException e) {  
        throw new RuntimeException(e);  
    }  
  
    System.out.println(numbers);  
}
```
---

- Why does the file still reach me if there's an issue when running OpenQKDNetwork in the office?
- Why does `qkd-kaiduan-a.tar` have B_0 and C_0 in it's `.qkd/qnl/qll/keys` dirs?

--
How does qkd-net's KMS handle multiple QKD connections? triangle with A,B,C.
