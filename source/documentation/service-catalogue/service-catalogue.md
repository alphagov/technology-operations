# Service catalogue

Here’s a sample service catalogue.

## Knowledge, code and story management

### Github

for collaboration on code, and storing of secrets in private repos.
User accounts created/deleted by GDS IT. Your team leaders can add you to relevant repos.

### Jira

the tool we are prioritising for story and issue management. Jira is our focus due to its excellent GDPR tooling and the ability to configure it for lots of workflows (including ISO/PCI compliant code reviews). We don’t want to use this ‘out of the box’, not least because we’re keen to measure baseline cycle time/MTTR across the whole of GDS and track improvements. Training will be made available in due course.

Note that Trello and Pivotal Tracker are not being assessed by IA and should not be used for any personal information including surnames.
Get Jira >

### Confluence

A wiki solution used by larger teams at GDS who have outgrown Google Drive.
400 licences have been procured. Approval by IA is in progress.

We would encourage you to involve your service and content design teams in any move to Confluence. Planning any template documents and the information architecture for your content is very important.
Get Confluence >

### Slack

Provided by GDS IT at gds.slack.com. Log in with your Google Apps account.
Remember Slack is subject to FOI requests. Find out more about acceptable use.

## Build systems and testing

### Jenkins2 Continuous Integration Server

Our build team are considering what new technologies we might adopt in this area. However, for now, there is a standard Jenkins2 build running on two ECS instances for teams to adopt. Securing this is hard; do not try and roll your own Jenkins.

Travis is used for some low-sensitivity projects such as documentation sites but is hosted in the US without US/EU privacy shield in place and becomes hard to manage on large projects.

Concourse is used on PaaS, but we do not wish other teams to adopt this yet.
No other tools should be used.
The team are seeking feedback from users, please contact them at #re-build-systems on Slack. You can also request some consultancy from the lead webops.
Request a Jenkins CI server for your project >
Request some CI consultancy>

### Secrets management

There is no software solution in place for this right now. Teams use private repos. MADE UP WORDS. We are looking at ways to manage this better in Q2->
Talk to #re-build-systems for more.

### Configuration patterns

There is no solution in place for this right now. Teams use dockerhub, S3 buckets, and more. MADE UP WORDS. We are looking at ways to manage this in Q3->
Talk to #re-build-systems for more.

### Artifact storage and deployment

There is no solution in place for this right now. Teams use dockerhub, S3 buckets, and more. MADE UP WORDS. We are looking at ways to manage this in Q3->
Talk to #re-build-systems for more.

### Release management

There is no solution in place for this right now. Teams use BEING CAREFUL. MADE UP WORDS. We are looking at ways to manage this in Q3->
Talk to #re-build-systems for more.

### Browserstack

Used by front-end teams to check their code in many browsers.
This has not been centrally procured. Discuss with the community lead (Matt Hobbs) and buy it on GPC if needed.
