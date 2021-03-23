# Dissonance: problem and goals

## Problem statement

1. All of the currently popular social networks are fully centralized. This leads to three major problems:
    1. The company is a single point of failure. Politically this allows for censorship and/or manipulation. Practically this means most of the content will be gone should the company fail for any reason or decide to retire a part of its features.
    2. Vendor lock-in. While all social networks allow for third party access, the APIs are usually artificially limited to prevent any kind of competition. This means the users are stuck with whatever possibilities their platform of choice has decided to provide.
    3. Data hoarding. The operating company has access to huge amounts of data, both public and private, and likely cannot or doesn't want to protect it from abuse.
2. A number of attempts at distributed communication platforms have been made over the years. To my knowledge, they all suffer from at least one of serious flaws that discourage most potential users:
    1. Most are server-based ("fediverse"), even if the network itself is decentralized. Any new potential user must pick a service provider before even starting to participate in the network. Specific communities may be locked in to a specific server. Moving an account afterwards can be difficult too.
    2. Self-hosting is an alternative but usually requires both technical knowledge and resources (an always-up machine with a public IP at the very least).
    3. Decentralization further increases disadvantage of having no "critical mass" as searching for interesting content or familiar people requires significantly more effort. Most users are likely to give up on the service even after signing up.
3. Many P2P technologies not originally created with social networking in mind exist. Earlier projects relied on "trackers" or "hubs" but now most employ some kind of a DHT.
    1. Most (all?) of these only allow "pulling" data, not subscribing or pushing.
    2. Most (all?) are built to share small numbers of large files and not a huge number of small blobs.
    3. No attempt to automatically orchestrate any persistence is made.
4. Overlay networks provide anonymity but solve none of the aforementioned problems.
5. Blockchains are misguided and unsuitable for any task.


## Goals

To alleviate some of the problems described above we should:

1. Define an open protocol for various forms of social networking:
    1. It should be simple but versatile, well-defined but extensible. A minimal implementation should be simple enough to replicate in a different context but able to handle any valid content in *some* useful way.
    2. It must be transport-agnostic and sessionless, and allow for both true peer-to-peer and client-server communication.
    3. It should be easy to inspect and tinker with but reasonably efficient (so probably binary but schema-less encoding compatible with JSON).
    4. It should use well-tested asymmetric cryptography solutions for both authentication and secrecy. No trust between peers is to be required at any point (optional key management services will be a separate protocol).
    5. All of the content and events on the network should be immutable and uniquely identified by its hash. Any updates are separate entities.
    6. Some kind of a DHT must be set up to locate copies of entities.
2. Develop a proof of concept implementation of all parts of the system.
   1. Protocol node implementation. Likely TypeScript to get to something runnable everywhere, fast. Pure core ES (no DOM or Node.js dependencies), abstract KV api for storage.
   2. Browser client implementation. Should be hosted somewhere but not tied to the server (use HTTP+CORS, WebSockets and WebRTC to reach out anywhere needed).
   3. Desktop client. Either an Electron wrapper for the web app (sucks) or a lightweight NodeGUI app with local web server for the app.
   4. Android/iOS clients. Least effort for full functionality would probably be WebView with native additions as needed and better local storage.
   5. Basic auth service for those who don't want to bother with key management themselves. We'd *want* everyone to do it, but we should also allow for a familiar login/password workflow with a trusted authority (but no monopoly).
   6. Some kind of a relay/archive server implementation (this is basically a node that is very eager to cache some or all of entities).
   7. Some kind of a gateway to link to for public posts that can fetch and return content and/or meta tags.
3. Set up an organization to handle basic centralized moderation tasks.
   1. We will have one or multiple "blocklists", which will essentially be a public feed of hashes of hashes of entities that we *believe* should be dropped from the network. This will generally be content universally agreed to be illegal.
   2. This list will be hard-coded into the client apps (but not the core), that is we will not provide an official way to opt out of said list. This is a significant measure of protection.
   3. We *may* create opt-in country-specific lists for public nodes to avoid them being blocked by said countries but this is not the main goal. The main goal is protecting the network and users from criminal abuse.

## Plan

TBD 🤣

