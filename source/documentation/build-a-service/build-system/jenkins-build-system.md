## Jenkins build system

The [Jenkins build system repository](https://github.com/alphagov/re-build-systems) provides examples for provisioning a Jenkins build system.

The build is a containerised [Jenkins (version 2)](https://jenkins.io/2.0/) platform on Amazon Web Services (AWS), consisting of a master node and an agent node. Once provisioned, users log into the Jenkins build using their GitHub account.

Read [Jenkins build documentation](https://github.com/alphagov/re-build-systems/tree/master/docs) for:

- architectural overview and decision records
- customising, reprovisioning, decommissioning, setting up a job
- Reliability Engineering - how to enable product team DNS
- Jenkins build system shared responsibility
