---
layout: post
title:  "Findings of the last month"
---

March 2023 is almost over, here I'll describe interesting things found for the last month.


### 1. Kubernetes events in K-Space Estonia
I am delighted to build stuff with an on-prem Kubernetes environment running on [K-SPACE](https://www.k-space.ee/), the Tallinn Hackerspace. 
It's a bare-methal solution, built on physical servers in place.

Key points:
* Drone for CI/CD
* Argo CD for GitOps
* A [series of talks](https://www.youtube.com/@k-space-ee/streams) dedicated to Kubernetes

Also, all participants got free remote membership for three months which provides access to the existing Kubernetes cluster, and the possibility of VM hosting on the infrastructure.
#### Conclusion: Strongly recommended to visit the place and have a look around 

### 2. [VU CYBERTHON 2023](https://ctftime.org/event/1881)


Yet another CTF challenge with a strong focus on forensics.
#### Example of a task

> What tank specs the user was looking for? 


> The main task is to perform the forensic information technology examination on the acquired image of mobile phone. Two suspects (two men) were arrested near Lithuanian and Republic of Belarus border. The truck with stored weapons was taken. During the seizure, a mobile phone without identification tags was founded on the ground near the truck. A criminal case has been opened related to the international illegal arms trade. Please help to find the relevant information for the case, examine the digital dump acquired from the seized phone memory and  answer the questions below. 


> What tank specs the user was looking  for? (provide model and name).

Participants needed to download the virtual image of the phone storage and perform forensics analysis over there. 

#### Conclusion: Absolutely brilliant CTF. Waiting for the write-ups comming soon.

### 3. Enabling Github Copilot in VS Code OSS
If you want to use the Copilot plugin in an open-source release of VS Code, you might face an issue, when the plugin complains about an "old version". 

However, the error is related to enabling specifc API in preferences.
In order to fix it, perform next steps:
* in command palette run `Preferences: Configure Runtime Arguments`
* add next value to the configuration:
```JSON
"enable-proposed-api": [
		"github.copilot"
	]
```

Now it works with no complains.