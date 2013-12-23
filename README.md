riak-ansible
===============

## Overview

This repository is a collection of configurations for running Riak
performance tests and inventories of specific test environments. It is
designed to be used with the ansible playbooks and the `arby` tool
that are found in the
[ansible-riak-benchmarking](https://github.com/basho/ansible-riak-benchmarking)
(or ARBY for short) repo.

The primary goal of this repo is to provide a repeatable means for
running benchmark tests against Riak that requires minimal effort on
the part of the tester in terms of test and test environment setup.  A
secondary goal is to provide an easy way to catalog the results over
time for future analysis and comparison.

This repo is organized as follows:

* Test configurations live in `configs/`. These tests are generic and
  may be used with any set of inventory data.
* Test suites are known as manifests and live in `manifests/`.
* Inventory data is configuration information for a specific test
  environment. This information lives in `inventories/`. An example
  inventory is maintained in `inventories/example/`.

## Setting up to test

1. Install ansible or clone the github repo
    * Ansible packages are available on `apt` and `yum`.
    * On OSX this can be done using homebrew: `brew install ansible`
    * Clone the github repo with: `git clone https://github.com/ansible/ansible.git`. There are some other python dependencies required when using the clone repo. Please see [this](http://www.ansibleworks.com/docs/intro_installation.html#running-from-source) for more details.
1. Clone `ansible-riak-benchmarking`: `git clone git@github.com:basho/ansible-riak-benchmarking.git`
1. Clone `riak-ansible`: `git clone https://github.com/basho/riak-ansible`
1. Create an inventory for a specific test environment
    * See `./inventories/example` for a guide.

## Basic Test Execution

To execute the *read-100KB-1hr* test the steps would be as follows:

1. `export ARBY_CONFIGS_DIR=PATH-TO-RIAK-ANSIBLE-REPO`
1. `export ARBY_INVENTORY_DIR=PATH-TO-RIAK-ANSIBLE-REPO/inventories/PATH-TO-DESIRDED-INVENTORY-DIR`
1. `export ARBY_GRAPH_GRAPHDEF=PATH-TO-ARBY-REPO/ansible-riak-benchmarking/utils/arby_graph/graph_definitions/combined.yml`
1. `export ARBY_REPORT_TEMPLATE=PATH-TO-ARBY-REPO/ansible-riak-benchmarking/utils/arby_report/templates/riak_report.md.j2`
1. `export ARBY_PROJECTS_HOME=PATH-TO-ARBY-REPO/ansible-riak-benchmarking/projects`
1. Run `PATH=PATH-TO-ARBY-REPO/ansible-riak-benchmarking/utils/bbenchmerge/bin:$PATH` or otherwise ensure `bbenchmerge.py` in on your path.
1. Run `PATH=PATH-TO-ARBY-REPO/ansible-riak-benchmarking/utils/arby_graph/bin:$PATH` or otherwise ensure `arby_graph.py` in on your path.
1. Run `PATH=PATH-TO-ARBY-REPO/ansible-riak-benchmarking/utils/arby_report/bin:$PATH` or otherwise ensure `arby_report.py` in on your path.
1. `cd` to `utils/arby/bin`
1. `./arby --test-config read-100KB-1hr`

See
[this](https://github.com/basho/ansible-riak-benchmarking/blob/master/docs/arby/using.md)
page for more details on `arby` and its options.

## Uploading results to S3 compatible storage

The test results can be uploaded to an S3-compatible storage
service. To ensure this works properly it is currently necessary to
have `s3cmd` installed and the default configuration file, `.s3cfg`,
must be configured to point to the storage service you would like to
use. Additionally you must have write access to the bucket specified
in the `s3` section of you inventory `groups_vars/all` file. For
example, to have results uploaded to the `riak-perf-testing` bucket on
S3, use the following configuration in your `group_vars/all`:

```
s3:
  report_path: riak-perf-testing
```

For those not familiar with S3, this requires that you must have first
created this bucket with a command such as `s3cmd mb
riak-perf-testing`.

## Testing custom Riak packages

**TODO**

## Using custom `beam` files for patch testing Riak

**TODO**

## Contributing

Please open an issue if you encounter problems or have ideas on how
this repo could be improved.
