# Vault Integration

## Abstract

We want utilized Hashicorp's Vault secret manager to store secrets as well as generate secrets on-demand for pods which require database credentials.

## Motivation

Secrets are difficult to manage in any system. Typical architectures utilize `service accounts` which are least privileged. The problem is that the passwords ties to these account rarely change, and multiple services utilize the same username and password. This leads to stale accounts and passwords which are infrequently updated and difficult to manage.

## Goal

We want a way where we can provision database credentials to MySQL for instance dynamically and they are used only for a single service instance.

## Non Goals

## High Level Architecture



- Some way to identify which containers in a pod need a vault authentication token and what kind of token it should be (policies) and optionally what environment variable it should be written to.
- Some idea where the vault service is and how to communicate with it (ssl certs etc)
- A token capable of issuing application tokens which is used by the plugin.
- A policy for how to handle errors – permission denied, service down etc.
- A way to rotate the issuing token and possibly renew
- Ability to attach any issued tokens to the correct container.

## Constraints

## Implementation Details
