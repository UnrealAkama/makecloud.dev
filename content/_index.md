---
title: Introduction
type: docs
---

# Makecloud


## What is Makecloud?

Makecloud is an open source CI/CD tool that is meant to make it easy to build software repositories in a simple manner. This is done so that it can intellegently stages in parallel and minimize the time that an individual run takes.

Makecloud is designed to work with large and complex source repositories, including monorepos, and other modern software development environments that deploy to directly to the cloud. The first and most significant design choice is to have Makecloud operate over a directed acyclic graph instead of pipeline or linear set of stages.

It does by using the built in artifact storage that handles both files and docker containers. This caching of artifacts serves multiple purposes. Builds finish faster, and it’s now possible to include base image generation in normal build pipeline and only update them when needed. Makecloud takes advantage of a project’s dependency graph to cache artifacts from stages whose dependencies have not changed since the last invocation, and to parallelize build stages when dependencies allow.

## Warning: BETA

Makecloud is complete enough that it can be used as a CI/CD system however it is still very much in beta. Please don't use it in production yet. It still has significant bugs. Mainly it can crash during runs and it can fail to delete virtual machines to clean up after it is done. As a friend once said, if it breaks, you get to keep both halves.

## CLI Support

Makecloud is written to be operator friendly and easy to use. The primary impact of this choice is that Makecloud has a CLI that is the primary usage tool. Makecloud can start runs and see all output from them without having to check in code to a central repository. Due to the built in caching and the cli first design, writing and testing single stages is a joy.

## Stage Isolation

Every stage in Makecloud is run on a separate virtual machine that has been spun up for just that purpose. This ensures that builds are not contaminated due to changes and allows the system to scale to execute as many stages in parallel as resources are available.

## Why OCaml?

Makecloud is written in OCaml because we think it is the best language to improve productivity and reduce bugs. Although the usage of OCaml in infrastructure tooling has been limited, there are excellent libraries to integrate with AWS EC2 and S3 which Makecloud uses heavily. In addition, by using Lwt as an async engine, writing the scheduler for Makecloud in a type-safe and preformant way became easy to do. Another nice advantage of using OCaml is the simple nature of using libraries under Dune. Dune has enabled Makecloud to be written as several different pieces that are nicely reusable: a library that contains all the core functionality, and both a cli and web server that use the library. This leads to a significant reduction in code reuse and fewer bugs overall.

## Overflow 

In addition, there are several features that make building code deployment graphs with Makecloud easy. There is built-in support for authenticated storage and retrieval of files and docker containers between stages so that user can focus on the important logic instead of plumbing. Configuration files are also simple and straightforward to use; most people can understand and write one with only a minute of explanation. Makecloud is run primarily as a web server that can be used as a CI/CD system with Github or other common tools with minimal configuration. Makecloud is also packaged as a command line tool that can be invoked locally without any other requirements. This makes it easy to tie into legacy systems as a method of running new CI/CD. Also, the ability to run as a command line tool allows engineers to test specific stages of the CI/CD pipeline with much less time spent per debug cycle than traditional setups allow.
