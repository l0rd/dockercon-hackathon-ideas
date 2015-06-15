## Compose Export

### DRY principle

We use and love Docker Compose in development environments. However in production we need to use some more sophisticated orchestration tools. As a result we have two distinct configuration files that describe the same containers relations.

To follow the [DRY principle](https://en.wikipedia.org/wiki/Don't_repeat_yourself) we need a tool transform a [compose yml file](https://docs.docker.com/compose/yml/) (used in dev environments) into a descriptor for the tools we use in production : 
* [Mesos Marathon recipes](https://github.com/mesosphere/marathon/blob/master/docs/docs/recipes.md)
* [Kubernetes pod configuration file](https://cloud.google.com/container-engine/docs/pods/operations#pod_configuration_file)
* [CoreOS fleet unit](https://coreos.com/docs/launching-containers/launching/fleet-unit-files/)
* A shell script

### Compose Export

To achieve that we could add a new Docker Compose command (`export`):
```
compose -f compose.yml export --format mesos-marathon
```
or build an application written in GO packaged as a docker image (`composexp`):
```
docker run -it composexp --file compose.yml --format mesos-marathon
```
or a web application that exposes some REST API to transform a yml/json from one format to anothe with a web UI form that make use of them.



