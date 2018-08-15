# Rfc 001 - Architecture Overview

## Introduction

Erudite Battles is a full open source game, the intention is to create a competitive educational game, using deck building and trading card concepts.

## Client

The full game client will be built using HTML5 and Ember.js framework, apriori the game will only only available through a web browser, but eventually should be portable into web containers and run them in multiple platforms (mobile, application, etc..).

## Server

The server will built in JAVA, using Spring framework. Will expose a REST Api, and to commmunicate actions on real time will open a socket interface with the clients through Web Sockets.

## Persistence

TODO: decided between SQL and NoSQL.

## Resources

Player accounts and resources should be managed through Ethereum smart contracts, this will give to the game a certain level of value.

## Deployment

We will use a Continuous Delivery approach, including running unit tests for building, integration tests, functional tests and deployment to QA vs Prod environments.
