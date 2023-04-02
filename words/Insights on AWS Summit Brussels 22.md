Originally posted on [[2022-04-06]] in 2 forms:
* Public: https://alkoclick.medium.com/insights-from-aws-summit-brussels-eed749b93d0
* Internal:  No link here ;)

Not for public disclosure until some filtering is done

---

AWS Summit Brussels 2022 is the first post-covid conference I attended. This document summarizes my insights from the conference.

## Schedule
 AWS Summit was a daily event and I attended the following presentations:
* Practical guide to incident response with NXP
* AWS Well-Architected Framework for sustainability
* Keynote
* Simplify cloud governance with AWS Control Tower
* Highly Regulated workloads on AWS
* ~~Build a zero-trust architecture on AWS~~ (I accidentally got in the wrong room so I watched about VMWare Tanzu instead)

Feel free to reach out if you'd like to discuss about the specifics of any presentation!

## Key Learnings
* Incident response (IR): 
	* Nearly impossible to do IR without a definition of a Cloud Consumer within the company, explicitly accountable as resource owner
	* It takes years to build and automate such a process, but you can start by just writing response playbooks after a few events and executing them manually
	* Don't forget the post-mortem! People often do
	* Plan to have security controls that cover both both Preventive (before) and Detective (after) measures
	* AWS has a managed service for IR: AWS Systems Manager Incident Manager. 
	* Responders who acknowledge an event can be required to provide some authentication (e.g an access code sent by mail). 
* Sustainability:
	* AWS has reduced their timeline for hitting net 0 carbon from 2030 to 2025. I'm not sure how much they're "cheating" (e.g buying CO2 credits) or just legitimately good at converting to renewable energy, probably both. Either way, climate targets seem poasible to hit and the industry is picking up steam.
	* AWS has released a report that allows you to see the total carbon footprint of your organization. Cloudflare also has such a report feature, I don't know about other providers 
	* Resilience and Sustainability may have opposite pulls in SLAs, prepare to balance them
	* Sustainability has been added as the 6th pillar of the AWS Well-Architected Framework
	* Sustainable scheduling: Reducing peaks optimizes your resource usage, schedule smartly to distribute load on low periods and vice-versa
	* Hardware patterns: Aim for 70-80% utilization in a CPU, Graviton=good, Graviton3=better
	* Data patterns: Optimize your log storage, set up deletion policies, consider ZSTD instead of Gzip/LZ4 as a compression algorithm
* Migrations:
	* KPN found it easier not to lift-n-shift but rather rebuild a lot of apps for the Cloud
	* Cloud Council of European Commission's position on cloud providers: "happy to stay, if we are free to leave"
	* (EU Commission) Serverless but **not** cloud native
	* (EU Commission) "The business people think 'our data is not safe in the cloud', the technicians think the opposite"
* Platform
	* Data Residency includes both storage and processing of data but people often forget or ignore the latter
	* GDPR compliance is much harder when you need to have people from different organizations working together
	* AWS LandingZone is no longer maintained
	* "Choose application" - "Choose dataset" - "Choose storage" are the 3 choices presented to cloud consumers at SURF
	* To help research orgs get in the cloud, SURF have the concept of "IT supporter", who is someone who helps the team onboard into tooling
* In a post-covid world, conference halls can fill up quickly. I entered the conf hall at 8:30, at 09:30 queues were longer than 30 minutes and at around 10:00 they locked the event. If I had gone with a daily train I would probably not have been able to make it. Being early a conference is pretty worth it in the current state of things.


## Thoughts & Actions
* We should review our carbon footprint report. I've skimmed our Cloudflare one already, but probably it's good to discuss both reports with the entire team. Possibly good to have an expert for insights as well
* I've asked VMWare when CloudHealth is expected to support Carbon Footprint information and to what granularity, and they told me they'd check their product roadmap and get back to me.
* I talked to Couchbase and they'd love to do a demo workshop to us on a Developer Day. Can we check if there is dev interest?
* We should really be looking into enabling AWS Config, GuardDuty and other resources with preconfigured rules. What is the best way to approach this?