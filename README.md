# crAPI

**c**ompletely **r**idiculous **API** (crAPI) will help you to understand the
ten most critical API security risks. crAPI is vulnerable by design, but you'll
be able to safely run it to educate/train yourself.

crAPI is modern, built on top of a microservices architecture. When time has
come to buy your first car, sign up for an account and start your journey. To
know more about crAPI, please check [crAPI's overview][overview].

## QuickStart Guide

### Docker and docker-compose

You'll need to have Docker and docker-compose installed and running on your host system. Also, the version of docker-compose should be `1.27.0` or above. Check your docker-compose version using:
```
docker-compose version
```

#### Using prebuilt images
You can use prebuilt images generated by our CI workflow by downloading the docker-compose and .env files.

 - To use the latest stable version.

      - Linux Machine

      ```
      curl -o docker-compose.yml https://raw.githubusercontent.com/OWASP/crAPI/main/deploy/docker/docker-compose.yml
      
      curl -o .env https://raw.githubusercontent.com/OWASP/crAPI/main/deploy/docker/.env

      docker-compose pull

      docker-compose -f docker-compose.yml --compatibility up -d
      ```

      - Windows Machine

      ```
      curl.exe -o docker-compose.yml https://raw.githubusercontent.com/OWASP/crAPI/main/deploy/docker/docker-compose.yml

      curl.exe -o .env https://raw.githubusercontent.com/OWASP/crAPI/main/deploy/docker/.env

      docker-compose pull

      docker-compose -f docker-compose.yml --compatibility up -d
      ```

      To override server configurations, change the values of the variables present in the .env file or add the respective variables to the start of the docker-compose command.   

      ```
      LISTEN_IP="127.0.0.1" docker-compose -f docker-compose.yml --compatibility up -d
      ```

  - To use the latest development version

      - Linux Machine

      ```
      curl -o docker-compose.yml https://raw.githubusercontent.com/OWASP/crAPI/develop/deploy/docker/docker-compose.yml

      VERSION=develop docker-compose pull

      VERSION=develop docker-compose -f docker-compose.yml --compatibility up -d
      ```

      - Windows Machine

      ```
      curl.exe -o docker-compose.yml https://raw.githubusercontent.com/OWASP/crAPI/develop/deploy/docker/docker-compose.yml

      set "VERSION=develop"

      docker-compose pull

      docker-compose -f docker-compose.yml --compatibility up -d
      ```

      - To Stop and Cleanup crAPI

      ```
      docker-compose -f docker-compose.yml --compatibility down --volumes
      ```

Visit [http://localhost:8888](http://localhost:8888)

**Note**: All emails are sent to mailhog service by default and can be checked on
[http://localhost:8025](http://localhost:8025)
You can change the smtp configuration if required however all emails with domain **example.com** will still go to mailhog.

### Vagrant

This option allows you to run crAPI within a virtual machine, thus isolated from
your system. You'll need to have [Vagrant] and, for example [VirtualBox]
installed.

1. Clone crAPI repository
   ```
   $ git clone [REPOSITORY-URL]
   ```
2. Start crAPI Virtual Machine
   ```
   $ cd deploy/vagrant && vagrant up
   ```
3. Visit [http://192.168.33.20](http://192.168.33.20)

**Note**: All emails are sent to mailhog service and can be checked on
[http://192.168.33.20:8025](http://192.168.33.20:8025)

Once you're done playing with crAPI, you can remove it completely from your
system running the following command from the repository root directory

```
$ cd deploy/vagrant && vagrant destroy
```

For more deployment options visit [the setup instructions](docs/setup.md) for more details.
---

To know more about challenges in crAPI. Visit [challenges]
----

[challenges]: docs/challenges.md
[overview]: docs/overview.md
[setup-k8s]: docs/setup.md#kubernetes-minikube
[vagrant]: https://www.vagrantup.com/downloads
[virtualbox]: https://www.virtualbox.org/wiki/Downloads

## Troubleshooting guide for general issues while installing and running crAPI
If you need any help with installing and running crAPI you can check out this guide: [Troubleshooting guide crAPI](https://github.com/OWASP/crAPI/blob/main/docs/troubleshooting.md). If this doesn't solve your problem, please create an issue in Github Issues.
