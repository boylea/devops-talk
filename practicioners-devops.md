theme:Ostrich-Salmon
footer: @amylouboyle
build-lists: true

# A DevOps Practitioners Guide


^ I'm a Lead software Engineer at New Relic working on the Core Data Platform, my team does real-time stream processing on the large amount of data my company ingests. 

---

## Every minute New Relic handles:

40M+ HTTP requests

1.8B+ new data points

1000T+ events queried

![fit left](NewRelic-logo-square-w.png)


^ To give a little context as to where I'm coming from, if you're not familiar with New Relic, we're a monitoring company. We're fully SaaS and multi-tenant.

^ As a member of a platform team, we aren't tied to a particular product, but support other product teams by providing a foundation to store and query customer telemetry data.

^ I'd like to know about you...

---

## Lead development teams?

___

## Are developers?

___

## Are on-call?

___
    
# **Ownership**

^ At the core of doing devOps well is fostering a sense of ownership. Teams own the whole lifecycle of their software, and suffer the joys and relish the consequences of what they produce. Development teams _want_ to take responsibility for what their application is doing in the wild because they have a sense of ownership end to end in the system. Ownership of one's work increases the team productivity and morale and makes for more reliable software.

___

# Ownership

* Owning software architecture and project work
* Owning observability
* Owning the deployment

^ I've divided the talk into three main themes. 

^ ...themes...

^ These really they aren't clean distinctions and contain a ton of overlap. It's kinda the point in fact, that we're blurring the lines between writing and deploying software.  However, I've hopefully grouped concepts in a way to make discussion a little more clear. 

___

# **Owning software architecture and project work**

<!-- ![](blueprint-ruler.jpg) -->

![right](https://cdn.pixabay.com/photo/2019/02/06/16/32/architect-3979490_960_720.jpg)

<!-- ![](construction.jpg) -->

<!-- ![](crane-with-blueprints.jpg) -->
^ Software teams produce better software when they have some control over what they are building. They should design their parts of the system and evolve it as they grow

^ We have an architecture team that is in charge of Platform/company-wide software architecture. Teams are in charge of building their piece of the system. They all have an architect to work with, who will be available as a resource and to ensure that the system as a whole is put together well.

^ We frequently have design meetings as a team in advance of starting project. Everyone on the team get a chance to weight in and participate. This is great for multiple reasons. One, engineer morale and engagement. Everyone on the team gets to feel a greater sense of ownership and accomplishment when they get to shape the work. Two folks from different backgrounds and different levels in their careers bring different perspectives to the table. A more junior engineer may ask a seemlying "basic" question that causes you to question your assumptions. Three is that it's part of leveling up the more junior members of the team. They get to see the thought process that goes into developing software architecture (including all the bad ideas and wrong directions), instead of just having it handed down already "figured out".

<!-- ^ Longer term planning is owned by the team tech lead and architect -->

<!-- ^ Specific example Metric-aggregators: came up with plan architect asked questions and we refined the plan. -->
<!-- https://pixabay.com/photos/blueprint-ruler-architecture-964629/ -->
<!-- https://pixabay.com/photos/building-construction-site-cranes-768815/ -->
<!-- https://pixabay.com/photos/shipyard-project-crane-construction-2458150/ -->
<!-- https://pixabay.com/photos/architect-people-plan-construction-3979490/ -->

---

# Designing for resiliency


^ At New Relic we care very much about reliability. We're not a "move fast and break things company", more of a "swiftly and safely". When software teams are on-call they have a very tangible stake in the resiliency of their software. Teams know what the toil feels like and don't want to waste their time on it. 

^ This can provide a negative feedback loop.  It's like your body, when you're sick...

___

![](football.jpg)

^ or injured you need to slow down and fix yourself. SOP can act like a car crash...

___

![](https://cdn.pixabay.com/photo/2016/08/25/20/14/crash-test-1620592_960_720.jpg)

^ ... like if a critical DB goes down. So we try to mitigate these things, like putting on a...

___

![](http://res.publicdomainfiles.com/pdf_view/35/13515677414616.jpg)


^ ... seat belt on by setting up data base replicas, and having failovers. 

<!-- ^ Don't always get this right. When you're the same people dealing with your mistakes in the wild you can learn faster.... -->

^ Ascribing to DevOps shortens this feedback loop, as the same team experiencing the ops pain has all the context of how the application was built and what was changed recently.


<!-- https://pixabay.com/photos/boo-swindon-town-football-pain-2399974/ -->

^ Of course, it's possible to get into a downward spiral and be stuck in fire-fighting mode. It's easier to deal with problematic code/services before they become a total tire fire.

---

# Teams deal with their own cruft and are empowered to fix it.

![left](decrepit.jpg)

^ We're always talking about engineering velocity at New Relic, and really good way to kill your velocity is to spend your time fire-fighting misbehaving services. _Most_ software was the right thing at the time, but we need to recognize when we need to take a time-out to fix or scales things to the next level.

^ We own a service which would snapshot snapshot state for recovery in failure scenarios. While the way this was implemented worked great at the time, as scale increased it was causing pages and a significant amount of the on-call engineers time. So we moved back feature work on our road map to immediately address the issue. We refactored the service to be more robust and more closely match other architecture in our system which snapshots state.

<!-- https://pixabay.com/photos/grain-elevator-decrepit-farm-880108/ -->

^ we don't have to wait for a service to start paging us to address the snakes nests in our code....

---

Maintainability is part of velocity

![](model-ferrari.jpg)

^ Maintainability is important for velocity and reliability. Software that is well maintained is easier to extend.

^ We try to follow a micro-services architecture. However, we had this service that because it was a convenient place to tack features onto, ended up doing 4 things instead of one. We were asked to further extend one of the these things, but at this point, we put the brakes on a little and first took time to extract it into it's own microservice instead of continuing to add complexity to the already overloaded service.

<!-- https://pixabay.com/photos/model-car-ferrari-model-mechanic-2099498/ -->

^ In addition to a strong support of reliability, a complementary philosophy is team ...

---

# Autonomy & collaboration

![](school-of-athens.jpg)

^ Autonomy (and a necessary framework for collaboration). Teams work better and have higher morale when they can make their own decisions about how to do their work

^ When you have autonomy it does mean that you need to make an intentional effort to avoid improper technology choices, information siloing or duplication of engineering effort that that are risks when you have high team autonomy

---

# Autonomy

<!-- ![](school-of-athens.jpg) -->

<!-- ![](collaboration.jpg) -->

![](https://cdn.pixabay.com/photo/2016/02/28/21/52/athletics-1227646_960_720.jpg)

^ Teams often have better information about what they can do to serve broad goals than central planners. Allow the domain experts to know which tools to use, and how to approach a problem

^ Team autonomy is huge at New Relic. As I've already mentioned teams own the design of their software, and this also includes the tools they use and processes at the team level. At least within reason. There are some rules you need to follow, like you must monitor your software with New Relic, and if you want to introduce new or obscure technologies you'll need to consult with the architecture team first. This mitigates technology choices that aren't maintainable outside that one expert or don't make sense for the org at large.

^ Avoid being blocked by other teams. Work around or implement things yourself if necessary. 

<!-- https://pixabay.com/photos/art-school-of-athens-rapha%C3%ABl-1143741/ -->
<!-- https://pixabay.com/photos/application-business-collaboration-3426397/ -->


^ Danger is duplicated effort, solving same problem multiple times across org. Not only duplicated, but done slightly differently everywhere. Each solution is rife with unnecessarily different details.

^ This doesn't always work out the best and we do still have a layer...

---

# Collaboration

![](https://upload.wikimedia.org/wikipedia/commons/thumb/c/c5/Rowing_Eights_Collegiate.png/800px-Rowing_Eights_Collegiate.png)

^ of coordination between what projects teams are working on. The Technical product managers for each team negotiate with each other about team roadmaps.

^ Communities of practice

^ Often discussed at these CoP meetings is the commons : we get this right, sometimes. We've standardized on kafka and have some well-maintained libraries associated with our usage patterns around it. 

^ example: kafka-clients compacted pattern. bug fixes

^ However, there are other libraries that are less well maintained and have no clear owner. This can cause issues when bug fixes need to be made, or when there is disagreement about the direction of where the code should go. I would try to avoid this state of having owner-less software.

^ In addition to code libraries. An area that should have a single clear owner is for...

<!-- https://commons.wikimedia.org/wiki/File:Rowing_Eights_Collegiate.png -->

---

# Collaboration

<!-- ![](containers.jpg) -->
<!-- ![](https://cdn.pixabay.com/photo/2016/04/04/14/12/monitor-1307227_960_720.jpg) -->

![](https://cdn.pixabay.com/photo/2017/11/08/15/04/computer-2930704_960_720.jpg)

^ infrastructure which all teams will need. You should have self-serve supported resources and libraries. Encourage most teams to use these things by making their jobs easier. For example New Relic has a Database team that will run a certain limited set of database types for you and manage the instances and replicas. Teams still own the schema and data.

<!-- https://pixabay.com/photos/business-cargo-containers-crate-1845350/ -->
<!-- https://pixabay.com/illustrations/monitor-binary-binary-system-1307227/ -->
<!-- https://pixabay.com/illustrations/computer-city-hack-network-digital-2930704/ -->

^ Before moving on to the next section, I'd like to talk about one guideline all teams at New Relic are strongly encouraged to follow...

---

Work on one thing at a time

![](many-thoughts-overwhelmed.jpg)

^ Have one active project at a time. It might be feature work, or scaling work or technical debt refactoring work. Everyone is working on the same project, keeps the time to delivery shorter so you can start getting feedback on things sooner and realizing the value sooner. 

^ Additionally it keeps the whole team in the same context which helps for collaborating on solutions and keeping the on-call up to date with recent changes. Team members avoid costly context switching trying to keep up with what the other folks on the team are working on for code reviews. It also avoid the knowledge silos you can get one each person has their own project. I've found it also tend to be more enjoyable. No one person gets "stuck" working on something, or no one person get to work on the exciting or high-profile project. The team is in it together.

^ There are always small timely tasks that come up and need to be done. We have a rotating role on the team we call ...

<!-- https://pixabay.com/illustrations/woman-girl-balloon-thought-bubble-1172718/ -->
<!-- https://pixabay.com/photos/upset-overwhelmed-stress-tired-2681502/ -->

---

Rotating hero handles distractions

![](https://cdn.pixabay.com/photo/2018/05/04/03/49/woman-3373173_960_720.jpg)

^the "hero" who, for a week at a time will work on time-sensitive issues, or maintenance issues to small to warrant a project. This person will also be responsible for fielding support questions. This is typically the same week as on-call. So there is one person on the team who is interruptible, allowing all others on the team to be able to focus on project work.

^ Downsides to single project work? What if there is not enough to parallelize on?

<!-- https://pixabay.com/photos/woman-super-hero-beautiful-3373173/ -->

___

# **Owning observability**

^ Of course sine we're responsible for the whole lifecycle of our software, we are responsible for making sure that we know how it's running, and that we know how we know it's running. That is, we understand our monitoring tools and are confident with the level of coverage we have. We know where to look to determine the health of the system, we know how to dive in and troubleshoot, and have alerts set up to automatically notify us when things go wrong.

^ Observability = thinking about monitoring holistically

^ Also means understanding you can't have perfect visibility, and being aware of your limitations. Particularly true in high throughput and distributed systems

^ We may approach monitoring from a few different...

---

# Motivations for monitoring

* Development
* Customer compassion
* Business intelligence

^ ... motivations. :cycle:

^ May overlap, in fact it can be good if they do

---

# Development

* Feature visibility
* Troubleshooting
* Capacity

^ This is probably the largest category

^ Did the thing I released work as expected? Did this refactor in fact not change anything?

^ What is happening with data flows/state? Errors.

^ Throughput and resource usage

---

![](nodestatus.png)

---

# Customer compassion

* Service quality
* SLAs

![](customer-experience.png)

^ latency
^ PSLIs 

---

# Business intelligence

* Who is using your product
* ROI

![](AccountDrilldown.png)

^ Which customers are the largest users of certain services?
^ decorate/join with ARR

^ Now that we've established why

---

# Things to monitor:

* System/application boundaries
* Decision points
* Bottlenecks
* Primary indicators of service quality

^ Distributed tracing/Kafka passport/PSLIs?

^ Decorate with useful things, metadata, dollars

^ Decision points: filter matching stats

^ Bottle necks: e.g queues, CPU utilization

^ Primary indicators for us: Data latency:lag (streaming systems key indicator; important because time to glass)

---

Keep monitoring asynchronous

^ e.g. MEE. Monitoring should be unobtrusive. Strive to keep it's impact small, do as little as possible in the hot path that will add to the latency experienced by customers. Extra processing and sends should happen in a background thread.
^ We make heavy use of APIs and custom instrumentation and keep this in mind.
^ Of course the New Relic agents are built upon this principle as well. I used to work on the Python Agent team, and doing the least amount of work possible while in the application code path was a foremost principle

---

# [fit] MELT

Metrics, Events, Logs, Traces

^ Use the right data type for the thing you're monitoring

___

# Metrics

* Pre-aggregated
* Lightweight

^ Metrics are pre-aggregated pieces of data that will give you measures like throughput, average, min, max. Good lightweight monitoring for the the hot-path in a high throughput system. You can decorate metrics with metadata to make them more useful, use them as dimensions you can group the metrics by. Need to be careful of cardinality explosions that can cause performance and storage issues.

---

# Events
 
* Point in time/sample
* Detailed

^ Events are pieces of monitoring recording a particular occurrence of something, a single timestamp with a bunch of associated data, typically key-value pairs. If these get to be high volume, they should be sampled. For example, we use events to record some details about start up, for error or for reporting sampled state such as JVM info or info on queues.

---

# Logs

---

# Traces

* Traces path across services

^ Trace the path of a request as it travels across a complex system, connecting the pieces
^ See where the slow component of your system is

---

# [fit] MELT

Metrics, Events, Logs, Traces

^ You'll use a combination of these things, with a mix that makes sense to you. On my teams we use events very heavily and have a plenty of metrics too.

___

# Monitoring-first mentality

^ Monitoring from first commit. If we're spinning up a new service we should be getting the basic health metrics we build into every service from our first push. Add a piece of functionality, ask your self, how do I know this is working?

---

Shared code? templates? Have your monitoring built into that.

^ Nos templates, Monitoring code in kafka-clients, MEE

^ Advantages:
     1. Monitoring is build in and already present
     2. Reduced effort/ code duplication
     3. Shared expertise of how to monitor the thing
     4. Common monitoring between teams for better shared understanding

---

# **Owning the deployment**

^ We deploy our changes in frequent small pieces
^ you should be the first one to know something is wrong with your system
^ Of course one of the great advantages to DevOps is that shortened troubleshooting loop and reduced MTTR. The team has all the context for debugging issues with their software plus access to and is knowledgeable about the system monitoring.

---

Playing nicely with others

![](https://cdn.pixabay.com/photo/2019/02/23/18/24/puppy-4016220_960_720.jpg)

^ GK Lets you know if someone else is having a bad time.
^ Used to block you when any dependencies were also going at the same time, but this got out of hand.

^ No matter how much you plan and test, you can never remove fault from your system...

<!-- https://pixabay.com/photos/puppy-labrador-retriever-play-dog-4016220/ -->

---

# [fit] Alerting

Unexpected problems that you need a human to fix

<!-- ![](https://cdn.pixabay.com/photo/2015/09/26/19/16/alarm-959592_960_720.jpg) -->
<!-- ![50%](https://upload.wikimedia.org/wikipedia/commons/5/59/Empty.png) -->

![inline, fit](https://cdn.pixabay.com/photo/2019/02/21/19/52/fire-truck-4012105_960_720.png)

^ Alerts are for humans, when something went wrong and requires thought to dig in and resolve. Any alert with a clearly defined runbook response should be automated away. Alerts should be actionable. It's been said many times before, but bears repeating since it still seems to be an issue. Mercilessly squish ...


<!-- ^ Ahead of the curve on alerting: partition ownership, sigkills, auto-commit failure -->
<!-- https://pixabay.com/photos/alarm-light-siren-emergency-959592/ -->
<!-- https://pixabay.com/photos/fire-truck-volunteer-firefighter-4012105/ -->

---

# [fit] Squish False Alerts

* Add allowed lateness
* Tune to be more or less specific
* Replace the alert
* Delete the alert

^ ... false positive alerts. If you're getting false positives because of late monitoring data, just wait longer. Alerts should be set up for response on human time scales, if you're needing to have a human respond, they are going to do so on the order of minutes in the fastest case. 

^ Alternatively, you may need to tune the alert to be more or less specific as appropriate; Getting rid of the alert altogether - you may want to consider what other signals you could use to alert on the the thing, the actual impact. Sometimes you just need to straight up delete the alert. It is not worth the cost of alert fatigue, when all your alerts then become less effective.

^ Every week we count the number of pages and how many were actionable. we review all the off hours pages for the week

^ We squished a noisy alert just last week on my team, we had set up a baseline alert on some traffic to detect swings in traffic that may indicate our service was losing or duplicating data. Well, it turns out the traffic to this service is actually pretty volatile and was not a good candidate for this type of alerting. So we deleted it. We added some other simpler rules that would just make sure there was a minimum flow per instance, and added another signal that would help us determine if there had been data duplication.


<!--

Add missing signals for alerts. FIXME: Needs more pithy

^ One of the great advantages to this ownership model is that the team getting paged has the power to add a signal, some extra monitoring, when it's missing. This can help with squishing false alerts, and also filling in gaps you discover.

^ A few months ago we added monitoring for sigkills.. (mention that sigkills are related to auto-deploys.)
 -->

^ So now you've got good, low noise, alerts coverage, what do you do when you get paged? You need to communicate efficiently with others involved engineering team and support. And if the impact is large enough, organization leadership as well.

---

Incident command

![](https://cdn.pixabay.com/photo/2013/06/02/23/13/firefighters-115800_960_720.jpg)

^ When we're experiencing an SLI violation we go the the #emergency-room to coordinate with other engineering teams and support
^ We have a whole central process we've put a lot of thought into. Deserves a whole talk, in fact some colleagues have given one titled...

<!-- https://pixabay.com/photos/firefighters-fire-flames-outside-115800/ -->

---

"Better Incident Management to Reduce MTTR"

___

![](https://upload.wikimedia.org/wikipedia/commons/thumb/3/3e/Stuck_Circle_dancing.jpg/624px-Stuck_Circle_dancing.jpg)

blameless culture fosters collaboration

^ Blameless incidents: If there is a fear of making mistakes and getting punished folks won't make critical decisions
^ Blame incentivizes excuses and avoiding the problem for folks who may have the power to fix it
^ Blameless retros : focus on process

---

Don't Repeat Incidents

![fit](https://cdn.pixabay.com/photo/2016/03/31/19/42/circle-icons-1295218_960_720.png)

^ Highest priority work
^ DRI and dealing with cruft are two parts of being empowered to fix your stuff and must be a part of DevOps and software ownership. 

___

It's not ownership if you're not allowed to fix it

^ You can't expect teams to own this stuff if they aren't allowed to fix it. If a team doesn't feel like they can maintain their service they don't really own it.

<!-- https://pixabay.com/vectors/circle-icons-dragon-ring-snake-1295218/ -->

<!--  
[.autoscale: true]

## If you remember nothing else....

* Treat maintainability as reliability
* Build monitoring into your system
* Mercilessly squish false positive alerts
* Don't repeat incidents
* Autonomy requires effective collaboration
-->

---

# **Ownership**

^ So to review a few of the main take-aways from his talk...
^ Ownership of one's work increases the team productivity and morale and makes for more reliable software.

---

# **Owning software architecture and project work**

* Treat maintainability as reliability
* Autonomy requires effective collaboration

---

# **Owning observability**

* Build monitoring into your system
* Share monitoring between teams

---

# **Owning the deployment**

* Mercilessly squish false positive alerts
* Don't repeat incidents


---
[.autoscale: true]

This document and the information herein (including any information that may be incorporated by reference) is provided for informational purposes only and should not be construed as an offer, commitment, promise or obligation on behalf of New Relic, Inc. (“New Relic”) to sell securities or deliver any product, material, code, functionality, or other feature. Any information provided hereby is proprietary to New Relic and may not be replicated or disclosed without New Relic’s express written permission.

Such information may contain forward-looking statements within the meaning of federal securities laws. Any statement that is not a historical fact or refers to expectations, projections, future plans, objectives, estimates, goals, or other characterizations of future events is a forward-looking statement. These forward-looking statements can often be identified as such because the context of the statement will include words such as “believes,” “anticipates,” “expects” or words of similar import.

Actual results may differ materially from those expressed in these forward-looking statements, which speak only as of the date hereof, and are subject to change at any time without notice. Existing and prospective investors, customers and other third parties transacting business with New Relic are cautioned not to place undue reliance on this forward-looking information. The achievement or success of the matters covered by such forward-looking statements are based on New Relic’s current assumptions, expectations, and beliefs and are subject to substantial risks, uncertainties, assumptions, and changes in circumstances that may cause the actual results, performance, or achievements to differ materially from those expressed or implied in any forward-looking statement. Further information on factors that could affect such forward-looking statements is included in the filings we make with the SEC from time to time. Copies of these documents may be obtained by visiting New Relic’s Investor Relations website at ir.newrelic.com or the SEC’s website at www.sec.gov. 

New Relic assumes no obligation and does not intend to update these forward-looking statements, except as required by law. New Relic makes no warranties, expressed or implied, in this document or otherwise, with respect to the information provided.
