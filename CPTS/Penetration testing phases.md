


## Importance

We must internalize this procedure and use it as a basis for all our technical engagements. Each stage's components allow us to precisely understand which areas we need to improve upon and where most of our difficulties and gaps in knowledge are. For example, we can think of a website as a target we need to study.

|**Stage**|**Description**|
|---|---|
|`1. Pre-Engagement`|The first step is to create all the necessary documents in the pre-engagement phase, discuss the assessment objectives, and clarify any questions.|
|`2. Information Gathering`|Once the pre-engagement activities are complete, we investigate the company's existing website we have been assigned to assess. We identify the technologies in use and learn how the web application functions.|
|`3. Vulnerability Assessment`|With this information, we can look for known vulnerabilities and investigate questionable features that may allow for unintended actions.|
|`4. Exploitation`|Once we have found potential vulnerabilities, we prepare our exploit code, tools, and environment and test the webserver for these potential vulnerabilities.|
|`5. Post-Exploitation`|Once we have successfully exploited the target, we jump into information gathering and examine the webserver from the inside. If we find sensitive information during this stage, we try to escalate our privileges (depending on the system and configurations).|
|`6. Lateral Movement`|If other servers and hosts in the internal network are in scope, we then try to move through the network and access other hosts and servers using the information we have gathered.|
|`7. Proof-of-Concept`|We create a proof-of-concept that proves that these vulnerabilities exist and potentially even automate the individual steps that trigger these vulnerabilities.|
|`8. Post-Engagement`|Finally, the documentation is completed and presented to our client as a formal report deliverable. Afterward, we may hold a report walkthrough meeting to clarify anything about our testing or results and provide any needed support to personnel tasked with remediating our findings.|




Stage 1: Pre-engagement

in this we will define scope.

Have a pre-engagment meeting

a kick off meeting

and before any of these can be discussed in detail a NDA must be signed



There are several types of NDAs:

| **Type**           | **Description**                                                                                                                                                                                         |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Unilateral NDA`   | This type of NDA obligates only one party to maintain confidentiality and allows the other party to share the information received with third parties.                                                  |
| `Bilateral NDA`    | In this type, both parties are obligated to keep the resulting and acquired information confidential. This is the most common type of NDA that protects the work of penetration testers.                |
| `Multilateral NDA` | Multilateral NDA is a commitment to confidentiality by more than two parties. If we conduct a penetration test for a cooperative network, all parties responsible and involved must sign this document. |
|                    |                                                                                                                                                                                                         |



## Scoping Questionnaire

After initial contact is made with the client, we typically send them a `Scoping Questionnaire` to better understand the services they are seeking. This scoping questionnaire should clearly explain our services and may typically ask them to choose one or more from the following list:

|||
|---|---|
|☐ Internal Vulnerability Assessment|☐ External Vulnerability Assessment|
|☐ Internal Penetration Test|☐ External Penetration Test|
|☐ Wireless Security Assessment|☐ Application Security Assessment|
|☐ Physical Security Assessment|☐ Social Engineering Assessment|
|☐ Red Team Assessment|☐ Web Application Security Assessment|

Under each of these, the questionnaire should allow the client to be more specific about the required assessment. Do they need a web application or mobile application assessment? Secure code review? Should the Internal Penetration Test be black box and semi-evasive? Do they want just a phishing assessment as part of the Social Engineering Assessment or also vishing calls? This is our chance to explain the depth and breadth of our services, ensure that we understand our client's needs and expectations, and ensure that we can adequately deliver the assessment they require.

Aside from the assessment type, client name, address, and key personnel contact information, some other critical pieces of information include:


This stage also requires the preparation of several documents before a penetration test can be conducted that must be signed by our client and us so that the declaration of consent can also be presented in written form if required. Otherwise the penetration test could breach the [Computer Misuse Act](https://www.legislation.gov.uk/ukpga/1990/18/contents). These documents include, but are not limited to:

|**Document**|**Timing for Creation**|
|---|---|
|`1. Non-Disclosure Agreement` (`NDA`)|`After` Initial Contact|
|`2. Scoping Questionnaire`|`Before` the Pre-Engagement Meeting|
|`3. Scoping Document`|`During` the Pre-Engagement Meeting|
|`4. Penetration Testing Proposal` (`Contract/Scope of Work` (`SoW`))|`During` the Pre-engagement Meeting|
|`5. Rules of Engagement` (`RoE`)|`Before` the Kick-Off Meeting|
|`6. Contractors Agreement` (Physical Assessments)|`Before` the Kick-Off Meeting|
|`7. Reports`|`During` and `after` the conducted Penetration Test|


Stage 2: Enumuration



You can use osint on Stack Overflow and github to try to find private keys or auth tokens. 

https://academy.hackthebox.com/course/preview/osint-corporate-recon

This is useful


Another essential step is `Pillaging`. After hitting the `Post-Exploitation` stage, pillaging is performed to collect sensitive information locally on the already exploited host, such as employee names, customer data, and much more. However, this information gathering only occurs after exploiting the target host and gaining access to it.

The information we can obtain on the exploited hosts can be divided into many different categories and varies greatly. This depends on the purpose of the host and its positioning in the corporate network. The administrators taking the security measures for these hosts also play a significant role. Nevertheless, such information can show the `impact` of a potential attack on our client and be used for further steps to `escalate our privileges` or `move laterally` further in the network.





Stage 3 (Vulnerabilities assessment


)

Any analysis can be very complicated, as many different factors and their interdependencies play a significant role. Apart from the fact that we work with the three different times (past, present, and future) during each analysis, the origin and destination play a significant role. There are four different types of analysis:

|**Analysis Type**|**Description**|
|---|---|
|`Descriptive`|Descriptive analysis is essential in any data analysis. On the one hand, it describes a data set based on individual characteristics. It helps to detect possible errors in data collection or outliers in the data set.|
|`Diagnostic`|Diagnostic analysis clarifies conditions' causes, effects, and interactions. Doing so provides insights that are obtained through correlations and interpretation. We must take a backward-looking view, similar to descriptive analysis, with the subtle difference that we try to find reasons for events and developments.|
|`Predictive`|By evaluating historical and current data, predictive analysis creates a predictive model for future probabilities. Based on the results of descriptive and diagnostic analyses, this method of data analysis makes it possible to identify trends, detect deviations from expected values at an early stage, and predict future occurrences as accurately as possible.|
|`Prescriptive`|Prescriptive analytics aims to narrow down what actions to take to eliminate or prevent a future problem or trigger a specific activity or process.|


Stage 4: Expoitation:

## Prioritization of Possible Attacks

Once we have found one or two vulnerabilities during the `Vulnerability Assessment` stage that we can apply to our target network/system, we can prioritize those attacks. Which of those attacks we prioritize higher than the others depends on the following factors:

- Probability of Success
- Complexity
- Probability of Damage

First, we need to assess the `probability of successfully` executing a particular attack against the target. [CVSS Scoring](https://nvd.nist.gov/vuln-metrics/cvss) can help us here, using the [NVD calculator](https://nvd.nist.gov/vuln-metrics/cvss/v3-calculator) better to calculate the specific attacks and their probability of success.


`Complexity` represents the effort of exploiting a specific vulnerability. This is used to estimate how much time, effort, and research is required to execute the attack on the system successfully. Our experience plays an important role here because if we are to carry out an attack that we have never used before, this will logically require much more research and effort since we must understand the attack and the exploit structure in detail before applying it.


Estimating the `probability of damage` caused by the execution of an exploit plays a critical role, as we must avoid any damage to the target systems. Generally, we do not perform DoS attacks unless our client requires them. Nevertheless, attacking the running services live with exploits that can cause damage to the software or the operating system is something that we must avoid at all times.


Prepping for the attack:

Sometimes we will run into a situation where we can't find high-quality, known working PoC exploit code. Therefore, it may be necessary to reconstruct the exploit locally on a VM representing our target host to figure out precisely what needs to be adapted and changed. Once we have set up the system locally and installed known components to mirror the target environment as closely as possible (i.e., same version numbers for target services/applications), we can start preparing the exploit by following the steps described in the exploit. Then we test this on a locally hosted VM to ensure it works and does not damage significantly. In other situations, we will encounter misconfigurations and vulnerabilities that we see very often and know exactly which tool or exploit to use and whether the exploit or technique is "safe" or can cause instability.




Lateral Movement:

## (Privilege) Exploitation

Once we have found and prioritized these paths, we can jump to the step where we use these to access the other systems. We often find ways to crack passwords and hashes and gain higher privileges. Another standard method is to use our existing credentials on other systems. There will also be situations where we do not even have to crack the hashes but can use them directly. For example, we can use the tool [Responder](https://github.com/lgandx/Responder) to intercept NTLMv2 hashes. If we can intercept a hash from an administrator, then we can use the `pass-the-hash` technique to log in as that administrator (in most cases) on multiple hosts and servers.

After all, the `Lateral Movement` stage aims to move through the internal network. Existing data and information can be versatile and often used in many ways.



For example, if a user uses the password `Password123`, the underlying vulnerability is not the password but the `password policy`. If a Domain Admin is found to be using that password and it is changed, that one account will now have a stronger password, but the problem of weak passwords will likely still be endemic within the organization.

## Documentation and Reporting

Before completing the assessment and disconnecting from the client's internal network or sending "stop" notification emails to signal the end of testing (meaning no more interaction with the client's hosts), we must make sure to have adequate documentation for all findings that we plan to include in our report. This includes command output, screenshots, a listing of affected hosts, and anything else specific to the client environment or finding. We should also make sure that we have retrieved all scan and log output if the client hosted a VM in their infrastructure for an internal penetration test and any other data that may be included as part of the report or as supplementary documentation. We should not keep any Personal Identifiable Information (PII), potentially incriminating info, or other sensitive data we came across throughout testing.

We should already have a detailed list of the findings we will include in the report and all necessary details to tailor the findings to the client's environment. Our report deliverable (which is covered in detail in the [Documentation & Reporting](https://academy.hackthebox.com/module/details/162) module) should consist of the following:

- An attack chain (in the event of full internal compromise or external to internal access) detailing steps taken to achieve compromise
- A strong executive summary that a non-technical audience can understand
- Detailed findings specific to the client's environment that include a risk rating, finding impact, remediation recommendations, and high-quality external references related to the issue
- Adequate steps to reproduce each finding so the team responsible for remediation can understand and test the issue while putting fixes in place
- Near, medium, and long-term recommendations specific to the environment
- Appendices which include information such as the target scope, OSINT data (if relevant to the engagement), password cracking analysis (if relevant), discovered ports/services, compromised hosts, compromised accounts, files transferred to client-owned systems, any account creation/system modifications, an Active Directory security analysis (if relevant), relevant scan data/supplementary documentation, and any other information necessary to explain a specific finding or recommendation further

At this stage, we will create a draft report that is the first deliverable our client will receive. From here, they will be able to comment on the report and ask for any necessary clarification/modifications.







