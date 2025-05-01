---
title: "Decentraland Platform Architecture"
slug: /contributor/architecture/platform
description: "Comprehensive overview of Decentraland's platform architecture, components, and services"
---

# Decentraland Platform Architecture

This document provides a comprehensive overview of the Decentraland Platform architecture, detailing its core components, services, and their interactions. The platform is built on a decentralized infrastructure that enables a persistent, shared virtual world.

![architecture](architecture.png)

## Table of Contents

- [Core Infrastructure](#core-infrastructure)
  - [Catalyst](#catalyst)
    - [Archipelago Service](#archipelago-service)
    - [NATS](#nats)
    - [LiveKit](#livekit)
    - [Lambdas](#lambdas)
    - [Content Server](#content-server)
    - [Nginx](#nginx)
  - [Realm Provider](#realm-provider)
- [Communication Infrastructure](#communication-infrastructure)
  - [Archipelago Workers](#archipelago-workers)
  - [Communications GateKeeper](#communications-gatekeeper)
- [Content Management](#content-management)
  - [Asset Bundles System](#asset-bundles-system)
  - [Worlds Content Server](#worlds-content-server)
  - [Atlas Server](#atlas-server)
- [User Services](#user-services)
  - [Auth](#auth)
  - [Social Service](#social-service)
  - [Badges System](#badges-system)
  - [Camera Reel](#camera-reel)
- [Development Tools](#development-tools)
  - [CLI](#cli)
  - [Catalyst Client](#catalyst-client)
- [Engagement Features](#engagement-features)
  - [Exploration Games](#exploration-games)
  - [Rewards](#rewards)
  - [Events API](#events-api)
  - [Places API](#places-api)
  - [Events Notifier](#events-notifier)

## Core Infrastructure

### Catalyst (Decentralized Content)

Catalyst servers form the backbone of Decentraland's decentralized infrastructure, providing essential services for content storage and distribution. These servers are responsible for maintaining the persistent state of the virtual world.

#### Key Components

- **Lambdas** ([Repository](https://github.com/decentraland/catalyst/tree/main/lambdas)): Provides utilities for Catalyst Server Clients/Consumers, including:
  - Data retrieval and validation
  - Blockchain ownership validations via Subgraph API
  - Service integration endpoints

- **Content Server** ([Repository](https://github.com/decentraland/catalyst/tree/main/content)): Manages decentralized storage for:
  - Scenes
  - Wearables
  - Emotes
  - User profiles
  - Automatic synchronization with approved servers

- **Archipelago Service** ([Repository](https://github.com/decentraland/archipelago-service)): Optional service providing client communication capabilities. Most nodes utilize external Archipelago Workers for the default Decentraland realm.

- **Nginx** ([Documentation](https://nginx.org/en/docs/)): Acts as a reverse proxy, managing traffic routing within Catalyst Services.

> **Note**: For running a Catalyst server, refer to the [Catalyst Owner](https://github.com/decentraland/catalyst-owner) repository. View available servers on the [Catalyst Monitor](https://catalyst-monitor.vercel.app/).

### Realm Provider

The Realm Provider service ([Repository](https://github.com/decentraland/realm-provider)) implements [ADR-110](https://adr.decentraland.org/adr/ADR-110), providing realm descriptions that specify the services required for client connections. It:

- Selects Catalyst and Lambdas services from the Catalyst Network
- Manages access to the default MAIN realm
- Coordinates with Archipelago Workers

## Communication Infrastructure

### Archipelago Workers

Archipelago Workers ([Repository](https://github.com/decentraland/archipelago-workers)) support standalone realms in Decentraland by:

- Implementing user clustering logic based on in-world positions
- Providing WebSocket connections
- Managing stats services
- Enabling real-time user interactions

### Communications GateKeeper

- [Comms Gatekeeper](https://github.com/decentraland/comms-gatekeeper):The comms-gatekeeper service acts as the guardian of LiveKit tokens within Decentraland's communication architecture. It processes signed fetch requests from clients and generates tokens that grant access to LiveKit rooms dedicated to specific scenes-rooms or worlds. Notably, LiveKit rooms for Archipelago follow a separate communication channel, ensuring proper routing and isolation (more dtails about the comms architecture in [ADR-204](https://adr.decentraland.org/adr/ADR-204)).

## Content Management

### Asset Bundles System

The Asset Bundle System generates optimized asset versions for the Catalyst network. Upon deployment of a scene, emote, or wearable, conversions are initiated for each platform (macOS, WebGL, Windows), with the Asset Bundle Registry updated to ensure the latest bundles are available.

- [Asset Bundle Registry](https://github.com/decentraland/asset-bundle-registry): Gateway for clients to retrieve available Asset Bundles and LODs, ensuring optimized textures and preventing empty scenes.
- [Asset Bundle Converter](https://github.com/decentraland/asset-bundle-converter): Processes deployments, uploads optimized versions to the CDN, and notifies the registry.
- [LODs Generator](https://github.com/decentraland/lods-generator): Processes scenes to generate versions with varying detail levels for resource-efficient rendering.

### Worlds Content Server

- [World's Content Server](https://github.com/decentraland/worlds-content-server) allows scenes to be uploaded using ENS NAMES instead of Genesis City LANDs. Worlds can be kept private or shared with others via a simple link. With the capacity to host up to 100 concurrent users, worlds can be utilized to host events, showcase work, or as a blank canvas to unleash creativity and experiment.

### Atlas Server

- [Atlas Server](https://github.com/decentraland/atlas-server): The Atlas service provides comprehensive information for the Atlas map, including details on roads, points of interest, land sales, and other essential data to enhance and beautify the Genesis City map.

## User Services

### Auth

- [Auth Server](https://github.com/decentraland/auth-server) Server in charge of communication between the decentraland desktop client and the [auth dapp](https://github.com/decentraland/auth) on the browser. Allows the desktop client to execute wallet methods (eth_sendTransaction, personal_sign, etc.) using the wallet the user has on their browser by leveraging the auth dapp.

### Social Service

- [Social Service](https://github.com/decentraland/social-service-ea): This service is designed to manage social interactions, including friendship lifecycle management, connectivity status, and user blocking.

### Badges System

The Badges service manages user achievements in Decentraland, guiding users through platform activities.

- [badges-api](https://github.com/decentraland/badges): Exposes endpoints for badge interaction.
- [badges-processor](https://github.com/decentraland/badges): Listens to events, updates progress, grants badges, and handles notifications.

### Camera Reel

- [Camera Reel](https://github.com/decentraland/camera-reel-service/) The Camera Reel Service is a simple solution designed specifically for uploading and retrieving camera images taken from Decentraland Explorer. This service enables users to capture and store images with additional metadata, providing valuable context to enhance their visual content.

## Development Tools

### CLI

The [CLI](https://github.com/decentraland/cli) provides tools and commands for scene development, including project scaffolding, local testing, and deployment to content servers.

**Repositories**:
- [CLI Source Code](https://github.com/decentraland/cli)
- [Examples and Tutorials](https://github.com/decentraland-scenes/Awesome-Repository)

### Catalyst Client

This [library](https://github.com/decentraland/catalyst-client) facilitates interactions with Decentraland's Catalyst servers, enabling data fetching and entity deployment.

**Repositories**:
- [Library Source Code](https://github.com/decentraland/catalyst-client)

## Engagement Features

### Exploration Games

- [Exploration Games](https://github.com/decentraland/exploration-games): The exploration games server is designed to create engaging challenges for users in Genesis City, encouraging world exploration and enhancing user engagement. It allows players to participate in various games, complete challenges, and earn rewards. This service tracks user progress across all available challenges, links to specific scenes in Genesis City where these challenges are hosted, and provides rewards to users upon completion.

### Rewards

- [Rewards](https://github.com/decentraland/referral): Rewards is a `closed-source` service available for public use that enables users to create campaigns featuring rewards, which can be claimed through dispensers added to various scenes. Content creators can utilize [the rewards service](https://decentraland.org/rewards/) to showcase their collections and reward users for attending events, completing challenges, participating in marketing campaigns, or simply for fun.

### Events API

- [Events](https://github.com/decentraland/events): This service integrates with the Events dApp, which is used to upload information about various happenings in Decentraland, providing visibility and discoverability for events such as the Metaverse Fashion Week, Metaverse Music Festival, Art Week, and any other user-hosted events.

### Places API

- [Places](https://github.com/decentraland/places): In addition to events, [Places](https://decentraland.org/places/) is another service focused on visibility and discoverability. It provides information about Decentraland scenes in both Worlds and Genesis City, allowing users to explore these scenes by category. Users can categorize and publish their own scenes, while the service also highlights the most active and popular locations based on user preferences.

### Events Notifier

- [Events Notifier](https://github.com/decentraland/events-notifier): This service is responsible for publishing blockchain events to internal systems. It runs cron jobs that analyze specific blockchain events and publish them to an event-driven architecture (SNS/SQS).