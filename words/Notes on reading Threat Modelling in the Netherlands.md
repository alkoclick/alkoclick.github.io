Originally retrieved from: https://www.ncsc.nl/documenten/publicaties/2024/mei/7/index

![](attachments/Threat%20Modeling%20KU%20Leuven.pdf)

> Threat modeling has no common definition and its focus (threats, threat actors, assets) varies among participants, yet is seen as an important activity by all.

> threat modeling serves a dual purpose: finding potential vulnerabilities, but also raising the security awareness among development teams.

>Finally, with regard to the process itself, participants perceive the value to be mainly in the process rather than in the quality of a threat model. That is, it is more important to do the analysis, rather than having a detailed and high-quality threat model.

> For the threat elicitation step, STRIDE is most frequently mentioned as the main driver for the threat elicitation.

> In most organizations, no strict follow-up processes for the results of threat modeling are in place. As part of such follow-up, positive feedback appears underused.

> Involving multiple architects during a threat modeling session to tackle this issue was also mentioned not to be favorable by one of the participants, as this may lead to lengthy discussions concerning the architecture. (“[...] the risk if you invite three architects to a session is that the discussions go in all directions. So then we prefer to have only the architect who is most involved there.”

> Measuring the effectiveness of threat modeling, and security in general, is indicated to be challenging (...) However, in order to create awareness and motivate teams to do threat modeling, being able to communicate its added value may be crucial

>In general, however, strict requirements for threat modeling are not advised as to prevent it from becoming a checkbox activity.

One tool that I see often brought up is "Threat Dragon"

> Participants recognize the opportunity for tooling and automation such as integration in CI/CD pipelines to trigger reassessments if changes may introduce new threats, but none of the organizations do so at the moment, mostly due to the lack of tool support

Build a startup in this space around an open source tool, get acquired by Snyk, profit

> Based on this study’s findings, the main advice for organizations is to consider and incentivize thinking about security in any shape or form, rather than mandating threat modeling and imposing strict requirements on the methodology.

> In general, a threat modeling session goes as follows. First, a facilitator from the security team provides an introduction of threat modeling, including an overview of the methodology (usually based on STRIDE). Then, a model of the system is constructed, the form of which ranges from whiteboard drawings to structured notations like data flow diagrams. Constructing a model may be time-consuming if architectural documentation is lacking. This model is subsequently analyzed, typically in a pragmatic manner. After the session, the facilitator creates a report which is distributed to the stakeholders. Follow-up is mostly ad-hoc, except when critical issues are identified. In general, this is a one-shot activity, but participants agree that threat modeling should be a continuous effort with periodic reassessments.

A neat outline of the common process structure