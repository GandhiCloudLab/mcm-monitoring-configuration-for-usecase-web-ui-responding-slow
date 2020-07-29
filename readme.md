# MCM Monitoring Configuration : use case -  Web UI Responding Slow

MCM leverages the following objects for Application Monitoring and Incident management.
- Thresholds
- Synthetic Tests
- Runbooks
- Event Policies
- Incident Policies

This document explains about how to create and configure those objects for an use case `Web UI Responding Slow`.

Here is the use case and incident handling flow.

<img src="images/026-response-flow.png">

## 1. Incident - Web UI Responding Slow

We are going to create and configure the following.

- Threshold for `Web UI service Response time high`
- Synthetic test for `Web UI service`
- Runbook for `How to Increase POD replica`
- Event Policies for `Web UI Response time high`
- Incident Policies for `Web UI Response time high`

Here is the sample incident with events and runbook.

### Incident Summary

<img src="images/017-incident-response-inbox.png">

### Incident Details - Events list

<img src="images/018-incident-response-events.png">

### Incident Details - Synthetic Test Event

<img src="images/019-incident-response-events-synthetic.png">

### Incident Details - Web UI Response time high Event

<img src="images/020-incident-response-events-response.png">

### Incident Details - Runbook associated
<img src="images/021-incident-response-events-runbook.png">

--------

## 2. Goto Administration Page in MCM Console

Click on the `Infrastructure Monitoring`

<img src="images/001-menu.png">

--------

## 3. Configuring Threshold

### 3.1 Goto Threshold Page

Click on the `Threshold` card

<img src="images/002-card-threshold.png">

### 3.1 Create Threshold for `Web UI service Response time high`

Here is the list of threshold created. You can click on `Create` button to create new.

<img src="images/003-threshold-home.png">

Here is the threshold configuration for `Web UI service response time high`.

Enter the parameters as highlighted.

```
Resource Type = Kubernetes Service
Lantency > 2000 milliseconds 
POD Name contains wealthcare-web
```

<img src="images/006-threshold-response-1.png">
<img src="images/006-threshold-response-2.png">
<img src="images/006-threshold-response-3.png">

--------


## 4. Configuring Synthetic Test

### 4.1 Goto Synthetic test Page

Click on the `Synthetic` card

<img src="images/031-card-synthetic.png">

### 4.2 Create Synthetic test for `Web UI service`

Here is the list of Synthetic Test created. You can click on `Create` button to create new.

<img src="images/007-synthetic-1.png">

Here is the Synthetic Test configuration for `Web UI service`.

Enter the parameters as highlighted.

```
GET URL : <application url>
Response Time > 1 seconds as warning 
Response Time > 2 seconds as Critical 
Interval : 10 seconds
```

<img src="images/007-synthetic-2.png">
<img src="images/007-synthetic-3.png">
<img src="images/007-synthetic-4.png">

--------

## 5. Configuring Runbook

#### Goto Runbook Page

Click on the `Runbook` card

<img src="images/008-card-runbook.png">

#### Create Runbook for `How to Increase POD replica`

Here is the list of Runbook created. You can click on `Create` button to create new.

<img src="images/009-runbook-replica-1.png">

Here is the Runbook configuration for `How to Increase POD replica`.

Enter the parameters as highlighted.

<img src="images/009-runbook-replica-2.png">
<img src="images/009-runbook-replica-3.png">
<img src="images/009-runbook-replica-4.png">
<img src="images/009-runbook-replica-5.png">
<img src="images/009-runbook-replica-6.png">

--------

## 6. Configuring Event Policies

### Goto Event Policies Page

Click on the `Policies` card

<img src="images/030-card-policies.png">

### Create Event Policies for `Web UI Response time high`

Here is the list of event policies created. You can click on `Create` button to create new.

<img src="images/010-event-home.png">

Here is the Event Policy configuration for `Web UI Response time high`.

Enter the parameters as highlighted.

- Here the `sender name` attribute value refers to the `synthetic test` we created in the previous step.
- Here the `summary` attribute value refers to the `threshold` we created in the previous step.

<img src="images/011-event-response-1.png">
<img src="images/011-event-response-2.png">
<img src="images/011-event-response-3.png">
<img src="images/011-event-response-5.png">
<img src="images/011-event-response-6.png">


#### Enrich

Here we enrich the event with `Application = Wealthcare UI Responding Slow`.

This event enrichment will ensure all the events with the `Application = Wealthcare UI Responding Slow` are correlated into one incident with the name `Wealthcare UI Responding Slow`

#### Runbook

Here assign the previously created runbook `How to Increase POD replica`

--------

## 7. Configuring Incident Policies

#### Goto Incident Policies Page

Click on the `Policies` card

<img src="images/030-card-policies.png">

#### Create Incident Policies for `Web UI Response time high`

Here is the list of Incident policies created. You can click on `Create` button to create new.

<img src="images/014-incident-home.png">

Here is the Incident Policy configuration for `Web UI Response time high`.

Enter the parameters as highlighted.

- Here the `Application` attribute value refers to the `Wealthcare UI Responding Slow` enrichment that was done in the previous step (event policy).

<img src="images/016-incident-response-1.png">
<img src="images/016-incident-response-2.png">
<img src="images/016-incident-response-3.png">

#### Group

Assinged the incident to `wealthcare group`.

#### Priority

Set the `priority 1` for this incident.

