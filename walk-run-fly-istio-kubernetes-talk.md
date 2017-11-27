%title: Istio London Meetup - Walk, Run, Fly with Istio
%author: https://control-plane.io  |  @lukeb0nd
%date: 2017-11-27


-> # Walk, Run, Fly with Istio <-

\                                 \_      \__  \_
                                (\_)\____/ /\_(\_)\___
                               / / \___/ \__/ / \__ \\
                              / (\__  ) /\_/ / /\_/ /
                             /\_/\____/\\\__/\_/\\\____/



-> Istio London Meetup <-
-> Skills Matter <-
-> November 27, 2017 <-


-> *Luke Bond* <-
-> *@lukeb0nd* <-
-> *luke@control-plane.io* <-

---

## The Problem Statement

> Companies want to release more often and with greater confidence, to get
> features in customers' hands faster and to encourage rapid experimentation
> and innovation within their company. Otherwise, they risk being overtaken by
> a more nimble competitor.

---

## The Postulate

> Cloud-native technologies are converging towards a set of tools that enable
> all the orchestration, deployment, monitoring, logging and networking
> features touted as best practice by the giants of the web, such as Google,
> Amazon, Facebook and Netflix. We have an idea of what the ideal model looks
> like.
>
> However, getting there is not easy for Enterprise companies with long-
> ingrained culture, workflow and tools.
>
> What we need is an upgrade path for Enterprises.

I'm going to propose that Istio is that path.

---

## What does this Ideal Model Look Like?

- *Intelligent Routing and Load Balancing*
  Control traffic between services with dynamic route configuration,
  conduct A/B tests, release canaries, and gradually upgrade versions using
  red/black deployments.
- *Resilience Across Languages and Platforms*
  Increase reliability by shielding applications from flaky networks and
  cascading failures in adverse conditions.
- *Fleet-Wide Policy Enforcement*
  Apply organizational policy to the interaction between services, ensure
  access policies are enforced and resources are fairly distributed among
  consumers.
- *In-Depth Telemetry and Reporting*
  Understand the dependencies between services, the nature and flow of
  traffic between them, and quickly identify issues with distributed tracing.

^
-> ## Sound Familiar? <-

^
-> *This is copy-pasted from _https://istio.io_* <-

---

## GIFEE

- This is the next step on the *GIFEE*
  - *Google's Infrastructure for Everyone Else*
- Enabled by Docker and Kubernetes, at the host and orchestrator level
- But now also networking, monitoring, logging, tracing and service meshes
  at a higher level
- Now we also have *Istio*, the biggest remaining missing piece, at the
  application level

-> Cloud-native has truly arrived! <-

-> It will soon be the norm for greenfield projects, if it isn't already <-

---

## What's so Great about Istio?

- Imagine you wanted to build the following across your microservices cluster:
  - Throttling, circuit-breaking and automatic retries
  - Tracing across routes touching multiple microservices
  - Programmable roll-outs supporting A/B, blue/green, red/black, etc.
  - Telemetry
  - Policy enforcement

You could write in-house libraries for this.
- In all the languages your company uses
- And maintain them
- For all your services and teams

The alternative is to do it with a service mesh; this is what Istio is.

- Istio achieves that by leveraging the _Envoy_ proxy (from Lyft)
- Envoy runs on each host and gets dynamically reconfigured by Istio

---

## The Great Microservices Lie

- Microservices have seen great success at many organisations
- Who here has seen a microservice mess?
  - Distributed monolith
  - No traceability
  - Tight coupling
  - Big-bang deployments
  - CV-driven-development
- It's not a lie of course, it's just hard

-> *Microservices success stories come from those who get these things right* <-

---

## Principles of Microservices

From *Building Microservices*, by Sam Newman (O'Reilly):

- Model around business concepts
- Adopt a culture of automation
- Hide internal implementation details
- Decentralise all the things
- Independently deployable
- Isolate failure
- Highly observable

Following these principles will ensure that you obtain the business benefits
of microservices and at the same time tame the complexity.

I'm going to pick out a few that are relevant to Istio.

---

## Adopt a Culture of Automation

- You will never be able to cope with the complexity of microservices with
  automating *everything*
- Every piece of un-automated technical debt will bite you hard at
  microservices scale
- Solutions that are "drop-in" and don't require custom libraries or explicit
  opt-in are a form of automation
  - Adoption automation, if you will!
- Istio gets this right

---

## Independently Deployable

- All these principles are important but this is perhaps the most important
- It's not really an operational concern, it's to iron out issues in your
  distributed system
  - It protects you from building a distributed monolith
- Your services need versioned APIs
- Your system needs to be able to handle multiple versions of a service running
  at once

---

## Isolate Failure

- A decentralised architecture is pointless if failures cascade across
  components
- You still need to design for failure, and consider the trade-off between
  constency and availability
- However, Istio has some features that help your microservices application be
  more robust:
  - Rate-limiting and related traffic features
  - Automatic retries can silently retry if a service fails
    - As the book says *don't treat remote calls like local calls*
  - Circuit-breakers can limit the fallout of a failing component
  - Gradual roll-out deployments can limit the damage of deploying a defective
    component

---

## Highly Observable

- Just like the automation point above, microservices will bite you at scale
  without high observability
- In fact, full automation *depends on it*
- Again, Istio helps you here:
  - Better understand your traffic flow with Istio's tracing
  - Programme Istio's service mesh to route synthetic traffic through your
    system and learn from the tracing

---

## Great! Where do I get Started with Istio?

^
-> *Not so fast!* <-

^
-> Didn't I tell you about the Great Microservices Lie? <-

^
-> What about the Great Istio Lie? <-

- You won't get the benefits of Istio without sorting some things out first
- If you do it prematurely, you'll cause yourself more harm than good
- Not everyone is ready to make the jump to Kubernetes, let alone Istio
- Many are still untangling a messy implementation of microservices

^
Building a successful microservices system- with many small services built by
multiple teams -requires a level of organisational and operational
transformation that is too-often left out of the discussion.

---

## The Upgrade Path

-> 1. _WALK_ <-

- Get your microservices house in order
  - Align services with business functions, and teams around services
  - Version your APIs; publish their contract
  - Ensure that teams who consume a service's API can develop against a
    version of it, unaffected by later upgrades
  - Be able to deploy services independently
  - Ensure multiple different versions of a given service can be deployed at
    the same time
  - Follow the *test pyramid*!
  - Each service should publish metrics
  - Develop post-deployment, non-destructive smoke tests to verify deployments

---

## The Upgrade Path

-> 2. _RUN_ <-

- Adopt a containerised workflow
  - Containerise your services
  - Test interactions between services locally, using containers
    - Test against the version of the service that you've developed against
  - Automate all this in CI; containerisation helps speed this up
- Don't forget your non cloud-native apps!
  - They're probably your bread and butter
  - Bring them into the homogeneous deployment artefact fold
  - Chip away at them with microservice replacements for parts of them
- Move to Kubernetes
  - If nothing else, it will make your deployments *much* easier
  - Also RBAC, secrets management

---

## The Upgrade Path

-> 3. _FLY_ <-

- Adopt Istio
  - With all of the above sorted, you're best-place to reap Istio's benefits
  - By the time you're ready for Istio, Istio will be ready for you!

---

## Conclusion

- Don't mess up the move to Istio like some people mess up microservices
- Get your microservice house in order
- Adopt containers and move to Kubernetes first



-> *Questions*? <-
