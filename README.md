# DevOps - Reference docs and skills

This is a quick, non-exhaustive list of documentation reference and skills required for a DevOps position.



## Overview

Main tools:

* terraform
* ansible
* git
* docker
* Jenkins

Important background:

* linux shell (bash or zsh)
* regular expressions
* json and yaml formats: syntax and how to automate querying and manipulating them through command line tools (jq and yq)
* md file format (for READMEs and similars in github)
* networking



## Shell scripting

* bash or zsh
* file redirection
* job control: bg, fg
* quoting & escaping
* options & arguments (meaning of `--` and correctly quote or escape arguments with spaces or special characters)
* regular expressions
* variables (scalar, arrays and associative arrays)
* join commands (`&&` and `||`)
* know specific functionalities of bash compared to posix shell, such as:
  - `[ expr ]` vs `[[ expr ]]`
  - <<<'here strings'
  - `*.{png,jpg}` and `{0..12}` brace expansion
  - process substitution with `<(cmd)` and `>(cmd)`
  - non-standard parameter expansions such as ${substring:1:2}, ${variable/pattern/replacement}, case conversion, etc.

Command line tools to know:

* ps
* kill
* lsof
* find
* grep
* sed
* awk
* cut
* tee
* networking tools: tcpdump, netstat, arp, dig, nslookup, telnet, traceroute, ifconfig/ip
* monitoring tools: top, htop, iotop, iostat, vmstat

Be able to pipe commands and filter their output. Understand the buffering and how to disable it when filtering streaming output (for example `tcpdump -l | grep --line-buffered`).

A good excercise could be to filter the output of `tcpdump` to provide simplified informations on the current network traffic.



## Linux

* main differences between distributions (Debian, RedHat, CentOS, Ubuntu), mainly regarding the package (apt/yum) and service managers (mainly `systemd` for all [new distributions](https://unix.stackexchange.com/questions/138994/init-systems-and-service-management-on-different-distributions))
* processes: states, PID/PPID, zombie processes
* control groups (for containerization technologies)
* file systems



## Networking

Understand and be able to describe:

* IP
* TCP vs UDP
* TTL
* HTTP/HTTPS protocol, included headers, methods (POST, GET, PUT, PATCH, and DELETE) and main [return codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)
* SSL/TLS
* DNS (DNS resolver, DNS root server, DNS TLD server, and DNS authoritative nameserver)
* POP/SMTP
* DHCP
* ARP
* swicth vs router

Be able to use the following commands:

* netstat
* arp
* tcpdump
* traceroute
* dig/nslookup
* telnet (for debug purposes) to test if a TCP port is listening
* wget/curl to test HTTP/HTTPS connections

A good excercise could be to try to make the following requests via `telnet` command:

* HTTP - `telnet <url> 80` and then providing the `GET` and `Host` command and header
* HTTPS - `openssl s_client -servername $HOST -connect $HOST:443` and then same commands as the previous one
* POP - `telnet <pop-server> 110` and send commands to list and show emails
* POP3S - `openssl s_client -connect <pop-server>:995` and the same commands as the previous one
* SMTP - `telnet <smtp-server> 25` and give the commands to send an emails
* SMTPS - `openssl s_client -CApath /etc/ssl/certs/ -crlf -starttls smtp -connect <smtp-server>:587` and then same commands as the previous one



## File formats

Know the syntax of yaml and json file formats.
Be able to query and manipulate json files with `jq` and yaml files with `yq`.
It's important to be able to write `md` files as well.



## Terraform

* [Best practises](https://cloud.google.com/docs/terraform/best-practices-for-terraform)
* modules
* providers
* backend
* variables types
* locals
* output
* dynamic blocks
* data sources
* `for_each` and `count`
* tfstate

Be able to describe the main files and structure of a terraform configuration: `outputs.tf`, `variables.tf`, `main.tf`, sub directories for modules, etc.



## Helm

Be able to manage repositories and install helm releases.
Be able to understand the content of an Helm chart:

* Chart.yaml
* values.yaml
* `charts/` directory
* `templayes/` directory



## GCP

There should be lots of documentation, some courses and labs for free. Some of them might be for a fee, but the ones for free should be generally enough.
I suggest to read the documentation and attend the courses related to the Google Associate Cloud Engineer certification, and become familiar with at least the most basic GCP services such as:

* VM
* instance groups/instance templates
* Cloud SQL
* GCS
* monitoring & logging (Google Cloud's operations suite) - just know which are the available functionalities
* know the main characteristics of the different data store services such as: Bigtable, BigQuery, Filestore, Datastore, etc (it's not needed to know them on depth)
* networking services: firewall rules, port forwarding, load balancers
* know the difference between all types of load balancers
  [Choose a load balancer](https://cloud.google.com/load-balancing/docs/choosing-load-balancer)
  it can be difficult to remember all load balancers types, but it's useful at least to know by what characteristics they differ

Documentation and courses:

* [Google Associate Cloud Engineer Certification](https://cloud.google.com/certification/cloud-engineer)
* [Preparing for Your Associate Cloud Engineer Journey](https://www.cloudskillsboost.google/course_templates/77)
* [Cloud Engineer Learning Path](https://www.cloudskillsboost.google/paths/11)

Labs:

* [A Tour of Google Cloud Hands-on Labs](https://www.cloudskillsboost.google/focuses/2794?parent=catalog)
* [Google Cloud Skills Boost](https://www.cloudskillsboost.google/)
* [QwikLabs](https://go.qwiklabs.com/)



## CI/CD

Be able to describe the workflow and stages of a CI/CD pipeline, such as (that's just an example):

* a change in a git repository trigger the pipeline (GitHub Actions or Jenkins)
* build: in case of a compiled language such as Java, the source code is compiled
* build artifacts are stored in a repository such as Nexus
* run unit tests (with Maven for a Java application, for example)
* security scans: vulnerability scan (Sonatype), SAST scan (Checkmarx)
* build docker image
* upload docker image to Nexus or other container registry such as `gcr.io`
* non-prod deployment with Helm in a non-prod GKE cluster
* run test automation tools: integration testing, regression testing, automated acceptance testing
* initiate Change Management to request the deployment on production (creating an `RFC` - request for change)
* production deployment with Helm to Prod GKE cluster
* in case of problem, rollback to previous version

Tools and concepts:

* Jenkins
* github actions
* continuous delivery vs continuous deployment
* deployment strategies: blue/green deployment, rollout deployment, canary deployment, staging environment
* test: unit testing, system testing, user acceptance testing, etc.



## Docker

Be able to:

* run a docker container
* access a docker container
* see the logs of a docker container
* create a docker container via Dockerfile 



## Git

Main commands and concepts:

* init
* checkout (also for creating new branches)
* add & commit
* push (also for pushing new branch to remote)
* pull
* diff (also between different branches)
* logs
* reset
* rebase vs fast-forward
* [status of files](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository) - untracked, unmodified, modified, staged



## SQL

Be able to write basic queries:

* SELECT
* DELETE FROM
* JOINS (inner/outer)



## Monitoring and alerting

Tools:

* prometheus & alertmanager
* grafana
* Google monitoring & logging



## Kubernetes

Kubernetes is difficult to master and I suggest to give precedence to other tools and technologies first.
I suggest to read about and be able to explain which are the main concepts and components:

* control plane
* worker nodes
* etcd
* config maps
* pods
* deployments
* services (different types)
* statefulset
* replicaset
* daemonset
* autoscaling
* volumes and volume claims
* secrets
* ingress & load balancing

Be able to install a local cluster and run some deployment and expose them through services is a plus.
I suggest to install a cluster on your workstation. You can use any of the following:

* https://docs.tilt.dev/choosing_clusters.html

I used `k3d` and Docker Desktop as local clusters.

After that, you can try to:

* create a deployment (nginx or some test app freely available)
* expose the application through a Service or an ingress
* access the pods via `kubectl exec`
* monitor the pods and other resources: logs, status, etc.

You can also try to create deployments through helm releases.

More advanced topics (not really required):

* operator model
* CRDs
* CSI Secret Store Driver



## Additional documentation

* https://12factor.net/
