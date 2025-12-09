# Explaining Local Observability Tools

Outline the Business Scenario
Business Scenario

Rotating Banana is a long-time SAP customer transitioning towards SAP S/4HANA and into the cloud. You will explore business scenarios from this hypothetical company for the remainder of this lesson about local Observability. Look out for the company logo to enter different roles and learn about their journey towards local Observability with SAP BTP.

Integrated Observability for SAP BTP Applications
You can use three main services to observe your SAP BTP applications:

SAP Cloud ALM serves for central (high-level) monitoring of BTP apps so that central support teams can detect problems as early as possible
SAP Cloud Logging serves for in-depth monitoring so that local DevOps teams can investigate the root-cause of problems
SAP Alert Notification service adds specific alert capture and propagation means, e.g., for app crash events.


![alt text](./images/DOP100_03_U4L3.png)

The interaction between the respective observability services may proceed as follows: a crash of a Cloud Foundry application is detected by SAP Alert Notification, which then triggers an alert in SAP Cloud ALM. Within SAP Cloud ALM, a support engineer notices related exception log messages. To understand the details behind these, they navigate in a context-sensitive manner into SAP Cloud Logging to examine all detailed log messages collected within the context of the exception.

Main Concepts: SAP Alert Notification Service for SAP BTP, SAP Automation Pilot, SAP Cloud Logging, SAP Cloud ALM
When providing and running applications in the cloud, Ops teams can encounter various issues and challenges within their cloud setup.

The following figure shows some examples of potential issues.
![alt text](./images/DOP100_01_U4L3.png)

Handling such challenges in time is critical for the reliable operation of any cloud application.

Therefore, SAP BTP provides the DevOps teams with the proper tools and services to keep their solutions up and running. They need to be notified about potential issues in time to do this.

Moreover, to cope with issues outside of working hours, DevOps teams need to automate remediation and recommended actions that can fix the issues.

Business Scenario

Our friends at Rotating Banana developed a cloud application deployed in SAP BTP, Cloud

Foundry environment. However, the app randomly becomes unstable and sometimes inaccessible for different users. To make matters more challenging, no alerts have been triggered so far. In this situation, a DevOps team should step in to tackle the problem.

As a member of the Ops team in charge of running this application, you are tasked to solve the issue by using local observability and operations tools in SAP BTP that complement SAP Cloud ALM as a central observability solution for SAP BTP:

SAP Alert Notification service (integrated with SAP Cloud ALM) with its primary focus on alerting
SAP Cloud Logging for an in-depth analysis of the root-cause
SAP Automation Pilot with its primary focus on ops automation

![alt text](./images/DOP100_01_U4L4C1_006.png)

Note

A previous lesson, "Introducing SAP BTP Services for DevOps," covered the capabilities of SAP Cloud ALM.
To implement notifications and automated remediation actions, you first need to understand the respective products and how they all work together in a fully integrated scenario. In the following sections, discover more details for both services before resuming the task in the Rotating Banana scenario.

As outlined before, the SAP Alert Notification service of SAP BTP collects crucial technical information from various sources and creates real-time events. The events are ingested into the service by SAP BTP applications and services, other products delivered by SAP, or by third-party tools and systems. Therefore, DevOps teams should regularly set conditions to filter out the relevant events, in interplay with SAP Cloud ALM, using the team's preferred channel of choice, or to trigger different predefined actions.

Setting up SAP Cloud Logging Service
Note

This lesson is geared mainly towards administrators, but any of the roles involved could benefit from it.
Business Scenario

As an SAP Business Technology Platform administrator at Rotating Banana, you have to plan and set up the local observability means for your organization, which can be realized via the SAP Cloud Logging service. For that you need an understanding about the use cases (such as workload monitoring, failure analysis, performance analysis) and stakeholders for local observability (such as Developers, DevOps engineers, Site Reliability Engineers, Operators) and derive the requirements to set up SAP Cloud Logging instances that meet the needs in terms of security, authorizations, isolation, usability, sizing, and cost efficiency.

Overview of SAP Cloud Logging
SAP Cloud Logging service is a comprehensive observability solution that serves application developers and operators to analyze their SAP Business Technology Platform workloads at full depth.

SAP Cloud Logging can be used for analysis and automated processing of observability data to better understand performance, errors, resource consumption, communication flows (traces), usage, and other observability characteristics.

It offers dedicated support for SAP BTP runtimes (Cloud Foundry / Kyma) for which smooth data ingestion paths and pre-built analytical dashboards are offered but also supports generic ingest APIs (OpenTelemetry, json) for ingesting logs, metrics, traces from arbitrary sources.

SAP Cloud Logging offers a rich and extensible analytical environment where users can slice and dice through the available data, add new visualizations and dashboards, and define rules for alerting and anomaly detection.

![alt text](./images/DOP100_coll03_U3L6_dashboard.png)

As an administrator of SAP Cloud Logging, you can determine the size and auto-scaling limits of your instance and control the authentication & authorization scopes of your users.

Defining Your Local Observability Goal
In order to derive your local observability goal, you should address the following aspects:

Scope: Clarify which workloads or other artefacts shall be subject to detailed local observation, i.e., shall emit observability signals to SAP Cloud Logging. This may also relate to different stages of your workloads, such as Dev, Test, or Prod. Last, you might also define overarching goals for what you need to observe for overall administration & operational purposes, including the related alerts you want to put in place.
Legal/Authorization Constraints: Clarify which data may reside in a common SAP Cloud Logging instance or requires the usage of SAP Cloud Logging in a specific region. Separating data into different instances is definitely the strongest isolation approach. However, you can also use different SAP Identity Authentication Service (SAP IAS) roles and index/document-level security features from SAP Cloud Logging to satisfy authorization constraints.
Joint Analytics: Check for scenarios where the joint analysis of multiple workloads would be beneficial, so that you would benefit from putting the observability data into the same instance.
Sizing (Ingest & Storage): Determine the volume of data that needs to be ingested and stored, including the required retention period. This will influence the number of instances, the appropriate service plan, and the limits to which you configure the auto-scaling of ingest and storage components. The service innovation guide and the capacity unit estimator will help you derive this information.
Operations: While shared SAP Cloud Logging instances may be beneficial in terms of analytics and cost, they also might create operational overhead on how to share such instances among multiple teams. The instance sharing guide will help implement this. The opposite approach might be to allow different teams to run their own SAP Cloud Logging instance.

![alt text](./images/DOP100_coll03_U3L6-clsSetup.png)

Setup of SAP Cloud Logging Instances
Based on your local observability goal, you should have a plan in which global accounts, sub-accounts and regions you want to set up SAP Cloud Logging instances.

The most important prerequisite is the setup of the underlying Identity Service and its authentication application as described in here. This will also cover the definition of groups and the assignment of admin users.
With that you can create the respective SAP Cloud Logging instances from the SAP BTP service marketplace, taking care that their security configuration (Security Assertion Markup Language - SAML) matches the setup in your Identity Service.
Application developers or workload owners can then bind to the respective service instance and start emitting observability signals. They can follow the SAP BTP Developer Guide possibly benefiting from the specific mission "Implement Observability in a Full-Stack CAP Application Following SAP BTP Developer’s Guide".

![alt text](./images/DOP100_coll03_U3L6-dev-guide.png)

Once SAP Cloud Logging instances are up and running, you may configure / use them to your specific needs, e.g.:

You may define specific alerts that support your administrative or operational goals.
You might even create own visualizations and dashboards that help you to oversee most relevant observability signals at a glance.

Set up SAP Alert Notification Service
The SAP Alert Notification service of SAP BTP collects crucial technical information from various sources and creates real-time events. The events are ingested into the service by SAP BTP applications and services, other products delivered by SAP, or by third-party tools and systems. DevOps teams can set conditions to filter the events out, thereby focusing only on the relevant ones.

The service supports an integration with SAP Cloud ALM, ensuring a seamless DevOps and Operations experience across your solutions. Otherwise, the SAP Alert Notification service for SAP BTP can deliver the events of your interest to a channel of your choice or trigger different predefined actions.
