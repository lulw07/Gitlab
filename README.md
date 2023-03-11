# Gitlab Configuration

I created a self-hosted [gitlab server](https://gitlab.lglomb.tech/). In this repository you will find all necessary Gitlab files for the pipleine.

## My Setup

I got an gitlab server and an deploy server.

The specs from the self-hosted gitlab vServer are:
* RAM 8
* vCPU 4
* Disk space 160GB

On this server I also let run the gitlab-runner in a docker container (DIND = Docker in Docker).


The deployment server only got:
* RAM 2
* vCPU 1
* Disk space 20GB

## Installation

To install a self-hosted gitalb server use [this youtube video](https://www.youtube.com/watch?v=H-XBVD1Y8Qs) and the [blog entry](https://blogs.perficient.com/2020/08/10/installing-and-configuring-own-gitlab-instance-in-ubuntu-server/).

To install the pipeline follow this DigitalOcean [tutorial](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-continuous-deployment-pipeline-with-gitlab-ci-cd-on-ubuntu-18-04).

To set up a shared runner simply take the same command for a normal project or group runner:

```gitlab-runner register --name my-runner --url <gitlab-server-url> --registration-token <group runner token>```

To find the group runner token go to teh Admin panel, then click on Groups and select your group. On the default the group is called `GitLab Instance`. If you selected the Group click on the Left Side-Bar on `CI/CD`. In the right corner you find the button `Register a group runner`. Copy the token and add it in the command above.