# Drone docker images for s390x

This is a monorepo where you can find all the images used on the drone pipeline for `s390x`
Some images are used on the pipeline itself ( github-release, slack, docker, git...) and other are used
on the components of drone ( cleaner and runner)

## Why
In order to run `drone` on `s390x`, we need to compile the code to the related architecture.
In this monorepo, you can find the different components and it's `Dockerfile`

## Triggering builds
To deliver new version of the components, is defined a `.drone.yml` which will be in charge of:
- Test if the build of the images are working ( It's performing only a build of the image)
- Publish the new image to the `rancher/drone-image` docker repository.

The publish step will be executed when a `tag` is created on `main` branch.

### Tag naming
Due to the characteristic of `drone` and our infra settings. We decided to follow the the next tag namming:
**v+version_number+-+component_name**

The **component_name** will determinate which folder will be selected to perform `docker build`

Examples:
- v0.0.1-git
- v1.2.5-slack
- v3.20.1-docker

### Docker images
The docker images are published under https://hub.docker.com/r/rancher/drone-images/tags
The tag will be the same that the one which triggered the pipeline plus a sufix **-s390x**

Examples:

|   Git tag         |   Docker image                                |
|:------------------|:----------------------------------------------|
|   v0.0.1-git      |   rancher/drone-images:v0.0.1-git-s390x       |
|   v1.2.5-slack    |   rancher/drone-images:v1.2.5-slack-s390x     |
|   v3.20.1-docker  |   rancher/drone-images:v3.20.1-docker-s390x   |

 