## Sibil Sarjam Soren

Backend engineer in Kolkata, currently a Senior Analyst at Accenture. I work mostly in Node.js and
TypeScript, on a piped natural gas platform that connects consumers to their regional
gas vendors.

Most of what I build sits behind an API — caching layers, job queues, notification
pipelines, rate limiters. I'm most interested in what a system does when something goes
wrong, which is usually where the actual design decisions are.

I came into software from mechanical engineering, so I learned this stuff by building
things and breaking them. That's still mostly how I work.

**Tech:** TypeScript · Node.js · Express · NestJS · PostgreSQL · Redis · MongoDB · React ·
Next.js · Docker · Azure

---

### Open source

Fixes I've had merged upstream, mostly around rate limiting, Redis and service restarts.

**[node-redis](https://github.com/redis/node-redis)**

- [Backported a reconnect fix to v5.12](https://github.com/redis/node-redis/pull/3622). Clients with more sharded channels than fit in one socket write never became ready after a reconnect. Shipped in `redis@5.12.3`.

**[rate-limiter-flexible](https://github.com/animir/node-rate-limiter-flexible)**

- [Fixed sub-second rate limits that never reset](https://github.com/animir/node-rate-limiter-flexible/pull/379). Durations under one second were stored with no expiry in Redis, Valkey and Memcache. Shipped in `v11.5.0`.

**[Openship](https://github.com/oblien/openship)**

- [Kept the service running when `openship up` runs again on macOS](https://github.com/oblien/openship/pull/1808). The CLI reported success while launchd had nothing loaded.
- [Stopped the API from outliving its supervisor](https://github.com/oblien/openship/pull/1809). A restart during startup left the old API holding its port and database lock.
- [Kept a running service on its own ports](https://github.com/oblien/openship/pull/1743). Running `openship up` again treated the service's own listeners as occupied and moved it to new ports.

---

### Projects

**[Gatekeeper](https://github.com/SibilSoren/gatekeeper)** — `npm i @sibilsoren/gatekeeper`

Rate limiting middleware for Express that stays correct across multiple instances. Most
rate limiters keep their counters in process memory, which quietly multiplies your limit by
the number of servers you're running. Gatekeeper keeps the counter in Redis and does the
check-and-increment inside a Lua script, so it stays atomic when several requests land at
once.

Three algorithms — fixed window, sliding window, token bucket. If Redis becomes
unreachable it falls back to in-memory counting instead of rejecting traffic, on the
argument that a rate limiter taking your API down is worse than a briefly imprecise limit.

[Docs](https://sibilsoren.github.io/gatekeeper/)

**[AudioPad](https://github.com/SibilSoren/audiopad)** — multi-track audio editor in the browser

The Web Audio API is imperative and React is declarative, so the real problem here was
keeping them apart. The audio engine lives entirely outside React and is driven by a Redux
middleware that translates actions into engine calls. Waveforms render to canvas rather
than the DOM, because drawing a few thousand peaks as elements does not go well.

[Try it](https://audio-pad.netlify.app/)

**[PixelUI](https://github.com/SibilSoren/pixelui)** — React component library

Built so I'd stop rewriting the same button, modal and input in every project. Components
extend the native HTML attribute interfaces, so `onClick`, `aria-*` and the rest pass
through the way you'd expect. Documented in Storybook.

**[create-api-starterkit](https://github.com/SibilSoren/create-api-starterkit)** — `npx create-api-starterkit`

Scaffolds a Node and TypeScript API with the tedious parts already wired: structured
logging, centralised error handling, Zod validation, Swagger docs, Docker. Came out of
setting the same things up one too many times.

**[Spinner-Zilla](https://github.com/SibilSoren/spinner-zilla)** — 13 loading spinners for React

TypeScript and Tailwind, no runtime dependencies. [Demo](https://sibilsoren.github.io/spinner-zilla/)

---

### Writing

I write up things I've had to work out properly, at
[sibilsarjamsoren.in/blog](https://sibilsarjamsoren.in/blog):

- [Availability Patterns: Fail-over and Replication](https://sibilsarjamsoren.in/blog/availability-patterns)
- [Understanding CAP Theorem](https://sibilsarjamsoren.in/blog/understanding-cap-theorem)
- [SOLID Principles Explained](https://sibilsarjamsoren.in/blog/solid-principles-explained)

---

### Elsewhere

[LinkedIn](https://www.linkedin.com/in/sibilsarjamsoren/) ·
[Website](https://sibilsarjamsoren.in/) ·
[soren.sibilsarjam@gmail.com](mailto:soren.sibilsarjam@gmail.com)
