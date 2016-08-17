# Vault Integration

## Abstract

We want utilized Hashicorp's Vault secret manager to store secrets as well as generate secrets on-demand for pods which require database credentials.

## Motivation

Secrets are difficult to manage in any system. Typical architectures utilize `service accounts` which are least privileged. The problem is that the passwords ties to these account rarely change, and multiple services utilize the same username and password. This leads to stale accounts and passwords which are infrequently updated and difficult to manage.

## Goal

We want a way where we can provision database credentials to MySQL for instance dynamically and they are used only for a single service instance.

## Non Goals

## High Level Architecture

- A token capable of issuing application tokens which is used by the plugin
- A policy for how to handle errors – permission denied, service down etc
- A way to rotate the issuing token and possibly renew
- Ability to attach any issued tokens to the correct container

## Constraints

- Need a way to identify which containers in a pod need a vault authentication token and what kind of token it should be (policies)
- What environment variable the initial token should be written (e.g. `VAULT_INIT_TOKEN`)

## Implementation Details

Utilize a custom admission controller (http://kubernetes.io/docs/admin/admission-controllers/) to inject an environment variable before the pod is scheduled onto a node. 
