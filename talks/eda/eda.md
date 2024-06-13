# Event-Driven Architecture
Learn from my mistakes



## Who am I
<img src="martin.jpeg" width="200px">

Martin Skovbo Faartoft

Lead Engineer @

<img src="lego_logo_srgb.svg" width="50px">

Get the slides: [ftft.dk/talks/eda](https://ftft.dk/talks/eda)



## Why am I here?
- I built a big distributed system
- Made every mistake in the book
notes: millions of events per day


## Events are easy


## Reliable events are <em>hard</em>
Don't repeat my mistakes!



## Distributed systems 101


## Your app will crash 
(at the worst possible time)


## The network is <em>not</em> reliable


### Synchronous
<div class="mermaid">
    <pre>
        %%{init: {'theme': 'dark', 'themeVariables': { 'darkMode': true }}}%%
        flowchart LR
            A[Service A] -- REQUEST --> B[Service B];
            B -- RESPONSE --> A;
    </pre>
</div>
notes: test


### Asynchronous
<div class="mermaid">
    <pre>
        %%{init: {'theme': 'dark', 'themeVariables': { 'darkMode': true }}}%%
        flowchart LR
            A[Service A] -- fa:fa-envelope--> B{{Broker}} -- fa:fa-envelope --> C[Service B];
    </pre>
</div>



## Things that went wrong
in no particular order



## Built my own framework
- Don't reinvent the wheel
- Use MassTransit/Rebus/NServiceBus/?



## Didn't understand configuration
- Screwed up ack/commit (check your defaults!)
<pre><code data-line-numbers>var e = await broker.Consume&lt;MyEvent&gt;();
var result = ComplicatedCalculation(e);
await broker.Publish(result);
await broker.Ack(e);</code></pre>


## different names
- Complete
- Commit
- Ack



## Screwed up Dual Write
- Outbox pattern
- CDC



## Trusted order of events
- Detour: dead-letters
- Dead letters
- Competing consumers
- Envelope timestamps
- Tombstones


##
![Distributed Systems Tweet](distributed-systems-tweet.png)


## Concurrency
- Lost update is really easy with wrong isolation level



## Didn't store processed events
- Explaining current state is _really_ hard without it



## Didn't apply Idempotency
- What is idempotency
- Detour: delivery semantics
- Sent a few too many emails



## No kill-switch
- Piling up >1M dead-letters over night.
    ``` C#
    services.AddKillSwitch(5, true, myClass)
    ```



## Accepted bad event formats
- Stitching partial events together
- Timestamps in local time
- Events with important data in envelope / headers
- PUSH BACK - LET THE PRODUCER KNOW



## Assumed ServiceBus pricing tier was easy to change



## Resources
- [Derek Comartin](link)
- [Designing Data Intensive Applications](link)



## Wordcloud
- Delivery Semantics
- Idempotency
- Dual Write
- Change Data Capture
- Two-Phase Commit
- Disitributed Transaction
- Transactional Outbox
- Dead letter
- Peek-lock
- Topics
- Queues
- Subscriptions
- Partitioning
- FIFO
- LIFO
- Exactly once delivery
- At least once delivery
- At most once delivery
- Exactly once processing
- Two Generals problem
- Failure Semantics
- Sync
- Async
- Eventual Consistency