## NABLA Jenkins slave Docker image

[![License](http://img.shields.io/:license-apache-blue.svg?style=flat-square)](http://www.apache.org/licenses/LICENSE-2.0.html)
[![Travis CI](https://img.shields.io/travis/AlbanAndrieu/ansible-jenkins-slave.svg?style=flat)](https://travis-ci.org/AlbanAndrieu/ansible-jenkins-slave)
[![Branch](http://img.shields.io/github/tag/AlbanAndrieu/ansible-jenkins-slave.svg?style=flat-square)](https://github.com/AlbanAndrieu/ansible-jenkins-slave/tree/master)
[![Donate](https://img.shields.io/gratipay/AlbanAndrieu.svg?style=flat)](https://www.gratipay.com/~AlbanAndrieu)
[![Ansible Galaxy](https://img.shields.io/badge/galaxy-alban.andrieu.eclipse-660198.svg?style=flat)](https://galaxy.ansible.com/alban.andrieu/eclipse)
[![Platforms](http://img.shields.io/badge/platforms-el%20/%20macosx%20/%20ubuntu-lightgrey.svg?style=flat)](#)
[![Docker Hub](https://dockerbuildbadges.quelltext.eu/status.svg?organization=nabla&repository=ansible-jenkins-slave-docker)](https://hub.docker.com/r/nabla/ansible-jenkins-slave-docker/)

- Requires Ansible 1.7.2 or newer
- Expects Ubuntu 

This playbook deploy a very basic jenkins slave with all the required tool needed for a developper or buildmaster or devops to work on NABLA projects.
This playbook is be used by [Docker Hub][3] to create a [Docker][1] image.

Goal of this project is to integrate of several roles done by the community. 
Goal is to contribuate to the community as much as possible instead of creating a new role.
Goal is to ensure following roles (GIT submodules) to work in harmony.

Then run the playbook, like this:

	ansible-playbook -i hosts -c local -v jenkins-slave.yml -vvvv
	or
	setup.sh

When the playbook run completes, you should be able to build and test any NABLA projects, on the using the docker image in Jenkins with [Jenkins Docker plugin][2].

This is a very simple playbook and could serve as a starting point for more complex projects. 

### Ideas for improvement

Here are some ideas for ways that these playbooks could be extended:

- Feel free to ask.

We would love to see contributions and improvements, so please fork this
repository and send us your changes via pull requests.

[1]: http://docker.io
[2]: https://wiki.jenkins-ci.org/display/JENKINS/Docker+Plugin
[3]: https://hub.docker.com
