# CircleCI Orb: send custom event to Splunk

Send notification event in `workflows` or `jobs` to your Splunk  

## Log event in Splunk

WIP

## Setup

This orb is available in both `workflows` and `jobs`.  

### Splunk setup

Create HTTP Event Collector (a.k.a. HEC) Token.  
Leave `index` and `sourcetype` default. They can be overwritten in this orb.

### CircleCI setup

#### workflow-event

```
version: 2.1
description: Send workflow event to Splunk
orbs:
  splunk: kikeyama/splunk@x.y.z
workflows:
  main:
    jobs:
      - splunk/workflow-event:
          subject: notificatoin from main workflow
          message: Successfully finisheed deploying to my cluster
          splunk_hec_host: ${SPLUNK_HEC_HOST}
          splunk_hec_port: 8088
          splunk_hec_protocol: https
          splunk_hec_token: ${SPLUNK_HEC_TOKEN}
          splunk_index: circleci
```

#### build-event

```
version: 2.1
description: Send build event to Splunk
orbs:
  splunk: kikeyama/splunk@x.y.z
jobs:
  build:
    docker:
      - image: <docker image>
    steps:
      - splunk/build-event:
          subject: notificatoin from build job
          message: Successfully finished build
          splunk_hec_host: ${SPLUNK_HEC_HOST}
          splunk_hec_port: 8088
          splunk_hec_protocol: https
          splunk_hec_token: ${SPLUNK_HEC_TOKEN}
          splunk_index: circleci
```

## Reference

For more details, see [orb registry](https://circleci.com/orbs/registry/orb/kikeyama/splunk)
