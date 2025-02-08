## dev:
* independent micro services
* self contained
* lightweight input endpoints with low latency, use message queues for async requests between services. this allows for resiliences and services can be brought offline in production for mantenance.
* use common database and message broker.
* code coverage should be at least 80% with a view to being 100% covered.
* testing pyramid must be followed: unit, integration and end to end tests
* 

## version control:
* trunk based development, anything merged to main needs to be deployed very soon before the next PR is merged to main.
* branches should be short lived and merged to main and deployed to production
* MR/PR should be reviewed by the entire team with one or two approvals
  * code review should be very strict, any optimisations must be discussed
  * code must  be very easy to read.
  * this can be frustrating for engineers who are new to this but the team will quickly adapt and standards with raise.

## QA
- regression suite for each microservice with all up stream and downstream dependencies tested too
- BDD testing using cucumber
- if testing API endpoints, make sure that rest calls are made to real QAT environment, test data should be added as part of the tests using create functionality via apis
- front end automatied test can be achieved using selenium and chrome driver running on build agent. use page object model.
-  test results should be published and linked to jira tickets via zephyr or xray
  
## CI/CD
- pipelines will automatically trigger on merge to main/master, the following stages will run:
  - checkout
  - build
  - test
  - package, increment major/minor version
  - deploy to nexus
  - docker build
  - upload container image to container image repository
  - deploy to k8s
  - run qa regression suite
  - if unsuccessful, rollback.
  - b/g site switch
  
## SRE

- build monitors and alerts,
- fine tune thresholds
- set SLA/Os
- work with engineering teams
- rightsize any hardware for cost
- monitor performance of service from a performance and cost perspective
  - raise issues witht teams
- monitor cloud log budgets and suggest optimisations to teams where too much logging is being made.
  - logs in prod, must be business flows and exceptions. linked with correlation ids. so that the journey from public endpoint can be traced through the entire platform and susequent hits to internal services traced.

# devops.

- own infrastructure iaas code base




