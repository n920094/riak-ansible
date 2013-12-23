riak-ansible
===============

## Overview

This repository is a collection of configurations for running Riak
performance tests and inventories of specific test environments. It is
designed to be used with the ansible playbooks and the `arby` tool
that are found in the
[ansible-riak-benchmarking](https://github.com/basho/ansible-riak-benchmarking)
(or ARBY for short) repo.

This repo is organized as follows:

* Test configurations live in `configs/`. These tests are generic and
  may be used with any set of inventory data.
* Test suites are known as manifests and live in `manifests/`.
* Inventory data is configuration information for a specific test
  environment. This information lives in `inventories/`. An example
  inventory is maintained in `inventories/example/`.

## Setting up to test

1. Install ansible or clone the github repo
1. Clone `ansible-riak-benchmarking`
1. Clone `riak-ansible`
1. Create an inventory for a specific test environment

## Test Execution

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
