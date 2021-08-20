---
description: Overview of DataHub's infrastructure
---

# 🏭 DataHub Infrastructure

## High Availability Architecture

DataHub uses a three-tiered system architecture with high availability at each layer.

1. Load balancing Ingress Layer
2. High availability Proxy Layer
3. Blockchain Node and Indexer Layer

Using this approach, we are able to provide a highly available service that can withstand multiple server failures at each level.

## Load Balancing Ingress Layer

All requests to `*.datahub.figment.io` are received and routed through a set of load balancers. This layer can tolerate failures of multiple individual load balancers and still function correctly.

The main job of this layer is to receive all inbound requests and terminate SSL before handing off to the Proxy Layer.

## High Availability Proxy Layer

Requests received at the Ingress Layer are then load balanced across a set of proxy servers at the Proxy Layer. This layer can tolerate failures of multiple individual proxy servers and still function correctly.

The main job of this layer is to authenticate requests, check Quotas and Rate Limits, and route requests to the correct service in the Blockchain Node and Indexer Layer.

## Blockchain Node and Indexer Layer

Requests authenticated at the Proxy Layer are then routed to the correct pool of blockchain nodes or indexers.

DataHub runs many different kinds of nodes and indexers, for example:

* Full nodes
* Archive nodes
* Higher level RPC/REST services \(like Cosmos LCD\)
* Services like Transaction Search

Each of these types of nodes is run as a pool, meaning for example there will be 5 identical copies of a full node running together that can all service requests. The pool can tolerate failures of multiple individual nodes and still function correctly.

The main job of this layer is to either:

1. Find and return the correct data \(read\)
2. Submit a transaction \(write\)

\*\*\*\*[**Sign up now**](https://datahub.figment.io/sign_up) \_\*\*\_to start building in minutes and discover the superpowers Datahub can offer you!

