## NABLA Jenkins slave Docker image

[![License](http://img.shields.io/:license-apache-blue.svg?style=flat-square)](http://www.apache.org/licenses/LICENSE-2.0.html)
[![Travis CI](https://img.shields.io/travis/AlbanAndrieu/ansible-jenkins-slave-docker.svg?style=flat)](https://travis-ci.org/AlbanAndrieu/ansible-jenkins-slave-docker)
[![Branch](http://img.shields.io/github/tag/AlbanAndrieu/ansible-jenkins-slave-docker.svg?style=flat-square)](https://github.com/AlbanAndrieu/ansible-jenkins-slave-docker/tree/master)
[![Ansible Galaxy](https://img.shields.io/badge/galaxy-alban.andrieu.eclipse-660198.svg?style=flat)](https://galaxy.ansible.com/AlbanAndrieu/ansible-jenkins-slave-docker)
[![Platforms](http://img.shields.io/badge/platforms-el%20/%20macosx%20/%20ubuntu-lightgrey.svg?style=flat)]()

# Table of contents

<!-- toc -->

<!-- tocstop -->

Requirements
------------

- Requires Ansible 2.9.4 or newer
- Expects Ubuntu

This playbook deploy a very basic jenkins slave with all the required tool needed for a developper or buildmaster or devops to work on NABLA projects.
This playbook is be used by [Docker Hub][3] to create a [Docker][1] image.

Goal of this project is to integrate of several roles done by the community.
Goal is to contribuate to the community as much as possible instead of creating a new role.
Goal is to ensure following roles (GIT submodules) to work in harmony.

Then run the playbook, like this:

    ansible-playbook -i hosts -c local -v jenkins-slave-docker.yml -vvvv
    or
    setup.sh

Then create the docker hub image, like this:

    docker build -f docker/ubuntu18/Dockerfile -t "nabla/ansible-jenkins-slave-docker" . --no-cache --tag "latest"
    or
    ./scripts/docker-build.sh

Run Jenkins See https://github.com/jenkinsci/parallel-test-executor-plugin/tree/master/demo

    docker volume create --name=m2repo
    sudo chmod a+rw $(docker volume inspect -f '{{.Mountpoint}}' m2repo)
    docker run --rm -p 127.0.0.1:8080:8080 -v m2repo:/m2repo -v /var/run/docker.sock:/var/run/docker.sock --group-add=$(stat -c %g /var/run/docker.sock) -ti jenkinsci/parallel-test-executor-demo

Then use the docker hub image, like this:

    #Pull image
    docker pull nabla/ansible-jenkins-slave-docker

    #Start container
    docker run -ti -d -w /sandbox/project-to-build -v /workspace/users/albandri30/:/sandbox/project-to-build:rw --name sandbox nabla/ansible-jenkins-slave-docker:latest cat
    #Build
    docker exec sandbox /opt/maven/apache-maven-3.5.0/bin/mvn -B -Djava.io.tmpdir=./tmp -Dmaven.repo.local=/home/jenkins/.m2/.repository -Dmaven.test.failure.ignore=true -s /home/jenkins/.m2/settings.xml -f nabla-servers-bower-sample/pom.xml clean install

    #Stop & remove container
    docker stop sandbox
    docker rm sandbox

When the playbook run completes, you should be able to build and test any NABLA projects, on the using the docker image in Jenkins with [Jenkins Docker plugin][2].

This is a very simple playbook and could serve as a starting point for more complex projects.

### Linting

```
ansible-lint -v playbooks/*.yml
```

[vault](https://github.com/ansible/ansible-lint/pull/991)

### Ideas for improvement

Here are some ideas for ways that these playbooks could be extended:

- Feel free to ask.

We would love to see contributions and improvements, so please fork this
repository and send us your changes via pull requests.

[1]: http://docker.io
[2]: https://wiki.jenkins-ci.org/display/JENKINS/Docker+Plugin
[3]: https://hub.docker.com

Update README.md Table of Contents
----------------------------------


  * [github-markdown-toc](https://github.com/jonschlinkert/markdown-toc)
  * With [github-markdown-toc](https://github.com/Lucas-C/pre-commit-hooks-nodejs)

`
npm install --save markdown-toc
`

### Contributing

The [issue tracker](https://github.com/AlbanAndrieu/ansible-jenkins-slave-docker/issues) is the preferred channel for bug reports, features requests and submitting pull requests.

For pull requests, editor preferences are available in the [editor config](.editorconfig) for easy use in common text editors. Read more and download plugins at <http://editorconfig.org>.

In lieu of a formal styleguide, take care to maintain the existing coding style. Add unit tests and examples for any new or changed functionality.

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

### Authors and license

`roles/alban_andrieu_jenkins_slave` role was written by:

- [Alban Andrieu](fr.linkedin.com/in/nabla/) | [e-mail](mailto:alban.andrieu@free.fr) | [Twitter](https://twitter.com/AlbanAndrieu) | [GitHub](https://github.com/AlbanAndrieu)

License
-------

- License: [GPLv3](https://tldrlegal.com/license/gnu-general-public-license-v3-%28gpl-3%29)

### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/AlbanAndrieu/ansible-jenkins-slave-docker/issues)!

***

This role is part of the [Nabla](https://github.com/AlbanAndrieu) project.
README generated by [Ansigenome](https://github.com/nickjj/ansigenome/).

***

Alban Andrieu

[linkedin](fr.linkedin.com/in/nabla/)
