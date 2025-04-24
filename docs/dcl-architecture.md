---
title: "Platform Overview"
slug: /contributor/architecture/platform
---

This document provides an overview of the Decentraland Platform architecture and its components:

![architecture](architecture.png)

## Table of Contents

- [Catalyst](#catalyst) 
  - [Archipelago Service](#archipelago-service)
  - [NATS](#nats)
  - [LiveKit](#livekit)
  - [Lambdas](#lambdas)
  - [Content Server](#content-server)
  - [Nginx](#nginx)
- [Catalyst Client](#catalyst-client)
- [CLI](#cli)

## Catalyst (Decentralized Content)

Catalyst servers bundle various services that form the backbone of Decentraland, providing decentralized storage for most of the content required by clients.

- [Lambdas](https://github.com/decentraland/catalyst/tree/main/lambdas): Offers utilities for Catalyst Server Clients/Consumers to retrieve or validate data, including ownership validations using the Subgraph API to query the blockchain.
- [Content Server](https://github.com/decentraland/catalyst/tree/main/content): Stores entities like scenes, wearables, emotes, and profiles, automatically syncing with other approved servers.
- [Archipelago Service](https://github.com/decentraland/archipelago-service) (Optional): Provides client communication capabilities, though most nodes rely on external Archipelago Workers for the default Decentraland realm.
- [Nginx](https://nginx.org/en/docs/): Functions as a reverse proxy to route traffic within Catalyst Services.

For running a Catalyst server, refer to the [Catalyst Owner](https://github.com/decentraland/catalyst-owner) repository. View available servers on the [Catalyst Monitor](https://catalyst-monitor.vercel.app/).

## Realm Provider

The Realm Provider service delivers a realm description ([ADR-110](https://adr.decentraland.org/adr/ADR-110)) detailing the necessary services for client connection. It selects any Catalyst and Lambdas service from the Catalyst Network and provides access to the default MAIN realm, managed by the Archipelago Workers.

[Repository](https://github.com/decentraland/realm-provider)

### Archipelago Workers

Archipelago Workers support a standalone realm in Decentraland, implementing clustering logic to group users by their in-world positions, and providing WebSocket connections and stats services.

[Repository](https://github.com/decentraland/archipelago-workers)

### NATS

NATS is a message broker facilitating data exchange and communication between services, enabling subject-based messaging for easy service connections.

[Project Link](https://nats.io/)

### LiveKit (SaaS)

LiveKit is an open-source project for scalable, multi-user conferencing over WebRTC, utilizing a Selective Forwarding Unit (SFU) for message relay and communication quality management.

[Project Link](https://livekit.io/)

## Asset Bundles System

The Asset Bundle System generates optimized asset versions for the Catalyst network. Upon deployment of a scene, emote, or wearable, conversions are initiated for each platform (macOS, WebGL, Windows), with the Asset Bundle Registry updated to ensure the latest bundles are available.

- [Asset Bundle Registry](https://github.com/decentraland/asset-bundle-registry): Gateway for clients to retrieve available Asset Bundles and LODs, ensuring optimized textures and preventing empty scenes.
- [Asset Bundle Converter](https://github.com/decentraland/asset-bundle-converter): Processes deployments, uploads optimized versions to the CDN, and notifies the registry.
- [LODs Generator](https://github.com/decentraland/lods-generator): Processes scenes to generate versions with varying detail levels for resource-efficient rendering.

## Badges System

The Badges service manages user achievements in Decentraland, guiding users through platform activities.

- [badges-api](https://github.com/decentraland/badges): Exposes endpoints for badge interaction.
- [badges-processor](https://github.com/decentraland/badges): Listens to events, updates progress, grants badges, and handles notifications.

## CLI

The [CLI](https://github.com/decentraland/cli) provides tools and commands for scene development, including project scaffolding, local testing, and deployment to content servers.

**Repositories**:
- [CLI Source Code](https://github.com/decentraland/cli)
- [Examples and Tutorials](https://github.com/decentraland-scenes/Awesome-Repository)

## Catalyst Client

This [library](https://github.com/decentraland/catalyst-client) facilitates interactions with Decentraland's Catalyst servers, enabling data fetching and entity deployment.

**Repositories**:
- [Library Source Code](https://github.com/decentraland/catalyst-client)

## Worlds Content Server 

- [World's Content Server](https://github.com/decentraland/worlds-content-server) allows scenes to be uploaded using ENS NAMES instead of Genesis City LANDs. Worlds can be kept private or shared with others via a simple link. With the capacity to host up to 100 concurrent users, worlds can be utilized to host events, showcase work, or as a blank canvas to unleash creativity and experiment. 

## Auth 

- [Auth Server](https://github.com/decentraland/auth-server) Server in charge of communication between the decentraland desktop client and the [auth dapp](https://github.com/decentraland/auth) on the browser. Allows the desktop client to execute wallet methods (eth_sendTransaction, personal_sign, etc.) using the wallet the user has on their browser by leveraging the auth dapp. 

## Social Service 

- [Social Service](https://github.com/decentraland/social-service-ea): This service is designed to manage social interactions, including friendship lifecycle management, connectivity status, and user blocking. 

## Camera Reel 

## Exploration Games 

## Rewards

## Communications GateKeeper  

## Events API 

## Places API 

## Events Notifier 