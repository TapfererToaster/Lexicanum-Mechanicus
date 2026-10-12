# Versioning and Changelog
## Versioning
A scheme for versioning is `major.minor.micro`, f.e. 2.7.1:
- `major`: adds backward-incompatible changes
- `minor`: adds backward-compatible features 
- `micro`: adds backward-compatible bug fixes

## Changelog
A changelog should contain information of what changed in a new version, f.e.
- Latest version number
- is the release backward compatible
- changes included in the new release
- release date of the previous version

# Monitoring
In monitoring there are two paradigms:
- push: f.e. [Graphite](https://graphiteapp.org/)
- pull: f.e. [Prometheus](https://prometheus.io/)

# Logging
## ELK Stack
The ELK stack consists of Elasticsearch, Logstash and Kibana. This allows to extract information from logs, capture metadata and send it to a document store (Elasticsearch), which is deisplayed on a dashboard (Kibana).

On most Linux distributions Elastisearch, Logstash and Kibana are not available, it is needed to import the right signing keys and configure the package manager to pull the packages from their repositories. [Ealastisearch](https://www.elastic.co/docs/deploy-manage/deploy/self-managed/installing-elasticsearch)

It is also advised to install Filebeat, a tool for log forwarding, which can be used to send logs to Logstash.

# Infrastructure as Code
**Pulumi** 
 [Pulumi](https://www.pulumi.com/docs/) is a IaC tool, that allows to define the desired state of infrastructure in a programming language like Python or Go.
This means it is possible to use functions, loops, etc. with describing what resources should be provisioned.
