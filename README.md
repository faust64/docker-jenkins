# Jenkins

Jenkins Template & set of custom Agents for OpenShift

```
$ oc process -f jenkins-agents.yaml | oc apply -f-
$ oc process -f jenkins-persistent.yaml | oc apply -f-
```
