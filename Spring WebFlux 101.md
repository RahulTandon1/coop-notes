**WebFlux in the overall Spring picture**
- Spring - set of tools/libraries (unopinionated; *React is not a framework* vibe)
- Spring Boot - opinionated take on how to use these ^ to build a webapp.
- We run into a roadblock with the `1 thread per request` model. Need async stuff like node provides. This does that.

**Why**
- Lambdas in Java -> continuation-style APIs

**Define reactive**
[ReactiveX](https://reactivex.io/)
- spans across programming languages
- *non-blocking back pressure* -> not sure what that means

https://www.reactive-streams.org/
- initiative, also lang independent
- has a separate github
- let subscriber control the speed of publisher producing data

**Reactive API**
- reactive streams too low-level; need an abstraction -> Reactor, (**and maybe RxJava too?**)
- input = Publisher -> `WebFlux API` -> output = Flux or Mono

2 programming models within Reactive stack:
- Annotated Controllers
- webflux-fn

Spring WebFlux *somehow* lets the user decide on:
- Server
- Programming model
- Reactive library - Reactor, RxJava etc.

> Mentions single-threaded Node's concurrency; cool!

Expected performance benefit: scale with fixed number of threads & less memory

**Concurrency model**
- different assumptions about blocking and threads
- thread-pool = event loop workers (**not sure what that means**)
---
- can use `publishOn` to call blocking code if required.

---

- HandlerFunction: `ServerRequest` -> `Mono<ServerResponse>`
- RouterFunction maps ServerRequests to HandlerFunctions