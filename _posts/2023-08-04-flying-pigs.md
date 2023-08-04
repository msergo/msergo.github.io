---
layout: post
title:  "Hazelcast Jet and the Sky Above: How I Tracked Air Traffic for Fun"
---

I made an app called Flying Pigs that pings me whenever an airplane saunters through the skies above my (mostly) Estonia-based headquarters. The sky, in my world, is just a simple square defined by a bunch of coordinates – simplicity at its finest.

As I became more aware of the many available flights, I chose to mute the notifier. The true enjoyment, as always, came from the development process, so the general conclusion is that the project was successful.

So far, it has been live for over 3 months, built as a few microservices, and is running on a Kubernetes cluster and Cloudflare Workers. In my opinion, the front-end is not necessary as I do not plan to create my own Flightradar24. Therefore, all notifications are sent to the [Telegram channel](https://t.me/FlyingPigsChannel).

![Telegram](/assets/flying-pigs-telegram.png).

While in the midst of development, I decided to throw in a [little map](https://flying-pigs-msergo.codemowers.ee/flight-map/7430f2a9-bf6b-436b-a25a-bd09b28bc4ff) for fun – you know, to visualize the flight path. Of course, real flights are more twisty-turny than a simple straight line. Think of it as a rough sketch for future ideas.


![the map](/assets/flying-pigs-map.png)

#### Now, the sweetest part. 

The backbone is a Hazelcast Jet pipeline, so it's written in Java. Actually, this was the main point of interest when building the project: to become familiar with the technology and see how nicely it behaves in the real (albeit small yet personal) world. I'd say it's a bit of a black sheep among data processing frameworks, but it's still very effective and easy to develop.
Thus, one can easily maintain a data processing project with very limited resources and a gentle learning curve.

In general, the data processing pipeline takes data from some kind of a <i>Source</i>, performs filtering/aggregating/calculating/magic stuff and outputs the result to a <i>Sink</i>. In my case, the source is a RabbitMQ exchange and the sink is a REST API backed with MySQL storage. The data is public; it is simply crawled from  [OpenSky](https://opensky-network.org/).

The beauty of having standardized interfaces is that you can easily replace different sinks and sources, just as you might swap tools in a toolbox. This means in tests, you can use the same data pipeline but output results to a console or fake storage.


Here are my general PROS:
* The Hazelcast Jet framework is open source, easy to start with, and has [decent documentation](https://jet-start.sh/docs/api/pipeline)
* It is lightweight, and one can start tinkering on an old laptop.
* Artifacts are built into a single JAR file, the good old Java way.
* The technology is very powerful and allows for building complex things.
* It is highly stable. So far, I haven't encountered crashes or hangs of jobs living in the cluster.
* Hazelcast Jetis designed to work in a distributed way, with job replication and fault tolerance also taken into account.

of course, some CONS
* In tests, it is assumed that the pipeline will throw a special CompletionException, so test job execution should be wrapped in a try-catch block.
* The management center is available as a premium feature only. So, for UI enthusiasts, it's an SSH journey to your cluster and checking job statuses via the CLI.
* Configuring a multi-instance [Jet cluster on Kubernetes](https://jet-start.sh/docs/operations/kubernetes#install-without-any-3rd-party-tool) is tricky if you are not having rights to update RBACs if the system. In my case I am not the maintainer of a k8s cluster, and the scope is limited to the namespace only. can be tricky if you lack the rights to update RBACs in the system. In my case, I am not the maintainer of the k8s cluster and my scope is limited to the namespace only. Eventually, I simply created two separate Jet services and pointed one to another using TCP configuration. So far, it's been good enough to go


```bash
$ k get svc
hazelcast-jet-service            ClusterIP      10.105.153.66    <none>           5701/TCP                                108d
hazelcast-jet-service-2          ClusterIP      10.99.209.38     <none>           5701/TCP                                92d
```
* Old good Java is a bit too old here. The only supported way to connect to RabbitMQ is by using JMS. Moreover, the maximum JVM supported version is 11. Not critical for me, but something worth considering.


My project also incorporates several secondary services: the REST API, the notifier, the OpenSky crawler, and supporting tools such as CI/CD integrations. By encapsulating the pipeline logic within distinct jobs, I am able to maintain a clean and easily transferable structure. Thus far, my experience with this technology has been exceptionally positive.


Source code of the pipeline implementation is available on [Github](https://github.com/msergo/flying-pigs-hazelcast). 