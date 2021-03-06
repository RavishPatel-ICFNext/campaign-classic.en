---
title: About Adobe Experience Manager
seo-title: About Adobe Experience Manager
description: About Adobe Experience Manager
seo-description: 
page-status-flag: never-activated
uuid: c523822f-8178-4989-bd88-ab402470e540
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: integrations
content-type: reference
topic-tags: adobe-experience-manager
discoiquuid: 0d617f1c-0d0b-489f-9027-a92b1f1eee37
---

# About Adobe Experience Cloud Triggers{#about-adobe-experience-triggers}

[!DNL Triggers] is an integration between Adobe Campaign and Adobe Analytics using the pipeline. The pipeline retrieves users' actions or triggers from your website. A cart abandonment is an example of trigger. Triggers are processed in Adobe Campaign to send emails in near real time.

[!DNL Triggers] run marketing actions within a short range of time following a user’s action. The typical response time is less than one hour.

It allows for more agile integrations since the configuration is minimal and a third party is not involved.
It also supports high volumes of traffic without impacting the performance of marketing activities. As an example, the integration can process a million triggers per hour.

## [!DNL Triggers] architecture {#triggers-architecture}

### What is Pipeline? {#pipeline-explanation}

>[!CAUTION]
>
>Only Adobe Cloud solutions can produce and consume events from Adobe’s Pipeline services. Systems that are external to Adobe cannot.

Pipeline is a messaging system hosted in the Experience Cloud that uses [Apache Kafka](http://kafka.apache.org/). It is a way to easily pass data between solutions. Further, Pipeline is a message queue rather than a database. Producers push events in the pipeline and the consumers listen to the flow and do what they want with the event. Events are kept for a few days but no more. The purpose is to listen 24/7 and process events immediately.

![](assets/triggers_1.png)

### How does Pipeline work? {#how-pipeline-work}

The [!DNL pipelined] process is always running on the Adobe Campaign marketing server. It connects to the pipeline, retrieves the events, and processes them immediately.

![](assets/triggers_2.png)

The [!DNL pipelined] process logs in to the Experience Cloud using an authentication service and sends a private key. The authentication service returns a token. The token is used to authenticate when retrieving the events. [!DNL Triggers] are retrieved from a REST web service using a simple GET request. The response is JSON format. Parameters to the request include the name of the trigger and a pointer that indicates the last message retrieved. The [!DNL pipelined] process handles it automatically.

## Using Adobe Experience Cloud Triggers integration with Adobe Campaign Classic

Here are a few [!DNL Triggers] best practices:

* The [!DNL Trigger] data needs to be stored as it comes in Campaign. It should not be processed directly as it would create latency.
* Timestamp should be checked from the message and not from the data base.
* Use TriggerTimestamp and trigger ID to remove duplicates.

>[!CAUTION]
>
>The example below is not provided out-of-box. This is a specific example from various possible implementations.

The pipeline events are downloaded automatically. These events can be monitored using a form.

![](assets/triggers_3.png)

The Pipeline Event node is not built-in and needs to be added, as well as the related form needs to be created in Campaign. These operations are restricted to expert users only. For more on this, refer to these sections: [Navigation hierarchy](../../configuration/using/about-navigation-hierarchy.md) and [Editing forms](../../configuration/using/editing-forms.md).

A recurrent campaign workflow queries on triggers and if they match the marketing criteria, it starts a delivery.

![](assets/triggers_4.png)
