[![CI](https://github.com/Shrey496/Ansible-Molecule-GitHub-Actions/actions/workflows/ci.yml/badge.svg)](https://github.com/Shrey496/Ansible-Molecule-GitHub-Actions/actions/workflows/ci.yml)


# Ansible-Molecule-GitHub-Actions
Continuous testing with Molecule, Ansible, and GitHub Actions.

# Description


## What is Molecule?

Molecule is a powerful framework for testing Ansible roles using various drivers such as Docker, Vagrant, or delegated environments. These scenarios are designed to demonstrate best practices for role testing, configuration validation, and local development workflows.

Each subdirectory under `molecule/` represents a self-contained Molecule scenario with its own configuration and tests.

It basically makes sure that the playbook actually does what it says it would do by simulating tests that would have to be done manually in order to test if the playbook works as expected.

## Prerequisites
* Access to GitHub

## CI/CD flow
1. Checkout repo
2. Set up Python & install Molecule/Ansible
3. Run **molecule test**
   * Creates a container (instance)
   * Applies Ansible role
   * Verifies behavior of the service
   * Destroys the test container 

## main.yml
* The structure consists of **Tasks**, **Handler**, and **Variables**
* Installs an Apache server on a Debian-based OS (determined by the OS of the container image in use)
* Has additional logic to accomodate for testing a Red Hat OS image (OS-agnostic)
* Add a simple HTML script within **/var/www/html/index.html**
* Restart Apache, and make sure it is up at boot

## molecule.yml
* Installs any dependencies via Ansible Galaxy
* Defines driver (eg: Docker)
* Chooses base image
* Defines instance settings
* Lints YAML and Ansible syntax

## converge.yml
* Updates package using the suitable package manager
* Imports **main.yml** file
* Installs and configures Apache within the test instance

## verify.yml
* It verifies the outcome of the test by sending a HTTP request to service URL (localhost in this case)
* Confirms if the output returns 200 OK


