---
title: "Platform"
slug: /contributor/architecture/platform
---

The following is a representation of the Decentraland Platform architecture and it's components: 

![architecture](architecture.png)

## Index

  - [Index](#index)
  - [Catalyst](#catalyst)
    - [Backend for Frontend (BFF)](#backend-for-frontend-bff)
    - [Archipelago Service](#archipelago-service)
    - [NATS](#nats)
    - [LiveKit](#livekit)
    - [Lambdas](#lambdas)
    - [Content Server](#content-server)
    - [Nginx](#nginx)
  - [CLI](#cli)
  - [Catalyst Client](#catalyst-client)
  - [Web Browser](#web-browser)
    - [Peer Library](#peer-library)
    - [Kernel - Voice Chat Module](#kernel-voice-chat-module)
    - [Kernel - Client Comms](#kernel-client-comms)
    - [Kernel - Scene Loader System](#kernel-scene-loader-system)
    - [Kernel - Scene](#kernel-scene)
    - [Kernel - Avatar Scene](#kernel-avatar-scene)
    - [Matrix Client](#matrix-client)
    - [Sagas](#sagas)
    - [Synapse](#synapse)
  - [Explorer Website](#explorer-website)
  - [Scene Runtime](#scene-runtime)
    - [Kernel - Runtime](#kernel-runtime)
    - [Compiler Bundle](#compiler-bundle)
      - [AMD](#amd)
      - [ECS](#ecs)
      - [User Code](#user-code)


## Catalyst

A Catalyst is a server that bundles different services. These services currently work as the backbone for Decentraland and run the decentralized storage for most of the content needed by the client and orchestrate the communications between peers. Some of these projects that are part of this bundle are:

- [Backend for Frontend](https://github.com/decentraland/explorer-bff) (BFF)
- [Archipelago Service](https://github.com/decentraland/archipelago-service)
- [NATS](https://nats.io/)
- [Lambdas](https://github.com/decentraland/catalyst/tree/main/lambdas)
- [Content Server](https://github.com/decentraland/catalyst/tree/main/content)

If you just want to run a Catalyst server, please check the [Catalyst Owner](https://github.com/decentraland/catalyst-owner) repository. 
You can check the list of available servers used by Decentraland in the [Catalyst Monitor](https://catalyst-monitor.vercel.app/)

### Backend for Frontend (BFF)

This service was created to resolve client needs to enable faster development of new features without breaking the existing APIs. In the Catalyst context, it's used for the communications between peers connected to the client, its main responsibility is to manage the P2P signaling. 

[Repo link](https://github.com/decentraland/explorer-bff)

### Archipelago Service

Previously Archipelago was a [library](https://github.com/decentraland/archipelago) used by the [Lighthouse](https://github.com/decentraland/lighthouse), as now it needs to work with the different transports beyond P2P, it was converted into a Service. This service will have the same responsibility that the library did: group peers in clusters so they can communicate efficiently. On the other hand, the service will also need to be able to balance islands using the available transports and following a set of Catalyst Owner defined rules, in order to, for example, use LiveKit for an island in the Casino and P2P in a Plaza.

[Repo link](https://github.com/decentraland/archipelago-service)

### NATS

NATS is a message broker that enables the data exchange and communication between services. This is also a building block for future developments and will enable an easy way to connect services using subject-based messaging. In the context of the communication services architecture, it is used to communicate the BFF, Archipelago and LiveKit.

[Project link](https://nats.io/)

### LiveKit

LiveKit is an open source project that provides scalable, multi-user conferencing over WebRTC. Instead of doing a P2P network, peers are connected to a [Selective Forwarding Unit](https://github.com/decentraland/comms3-livekit-transport) (SFU) in charge of managing message relay and different quality aspects of the communication. This will be the added infrastructure in order to provide high-performance/high-quality communications between crowds on designated scenes.

[Project link](https://livekit.io/)

### Lambdas 

This service provides a set of utilities required by the Catalyst Server Clients/Consumers in order to retrieve or validate data.
Some of the validations run in these functions are ownership related and for that it uses [The Graph](https://thegraph.com/hosted-service/subgraph/decentraland/collections-matic-mainnet) to query the blockchain. 


### Content Server 

The Content Server currently stores many of the [Entities](https://github.com/decentraland/common-schemas/tree/main/src/platform) used in Decentraland. For example scenes, wearables and profiles. Content servers will automatically sync with each other, as long as they were all approved by the [DAO](http://governance.decentraland.org/).

If you set up a local content server, it will receive all updates by those other DAO Catalysts. However, new deployments that happen on your local server will not be sent to other servers.

### Nginx

[Nginx](https://nginx.org/en/docs/) is the reverse proxy used to route traffic to the Catalysts Services.

## CLI

This [CLI](https://github.com/decentraland/cli) provides tooling/commands to assist you in the [scenes](https://github.com/decentraland-scenes/Awesome-Repository) development process. Some of the commands will help you scaffold a new scene project, locally start and visualize the scene in order to test it and deploy it to a content server to be incorporated in your Decentraland parcel.

**Repositories**:
- CLI Source Code: https://github.com/decentraland/cli
- Examples and Tutorials: https://github.com/decentraland-scenes/Awesome-Repository

## Catalyst Client

This client [library](https://github.com/decentraland/catalyst-client) can be used to interact with Decentraland's Catalyst servers. You can both fetch data, or deploy new entities to the server you specify.

**Repositories**:
- Library Source Code https://github.com/decentraland/catalyst-client

## Web Browser

**Repositories**:
- Explorer https://github.com/decentraland/explorer
- Kernel https://github.com/decentraland/kernel
- Peer library https://github.com/decentraland/catalyst-comms-peer 
### Peer Library 

The [Peer Library](https://github.com/decentraland/catalyst-comms-peer) manages Websocket connections for WebRTC signaling, Islands, Notifications and Location Data and WebRTC Connections for peers positions, scene bus, global chat and voice chat (private chat goes through the Matrix Synapse Server and the Matrix Client). 

**Repositories**:
- Library Source Code https://github.com/decentraland/catalyst-comms-peer
- 
### Kernel - Voice Chat Module

This [Module](https://github.com/decentraland/explorer/tree/af59463dd3882516874c86bc926726bc557d5184/kernel/packages/voice-chat-codec) is the codec to hook WebAudio & Worklets to comms
 
### Kernel - Client Comms

[Abstraction](https://github.com/decentraland/explorer/tree/df1d30412dcd1a94d933171a39796837aedc87a1/kernel/packages/shared/comms) over the Communication Protocol 

### Kernel - Scene Loader System

[Module](https://github.com/decentraland/explorer/tree/df1d30412dcd1a94d933171a39796837aedc87a1/kernel/packages/decentraland-loader) that loads and unloads the scenes/parcels based on user position.

### Kernel - Scene

High level [wrapper](https://github.com/decentraland/explorer/blob/af59463dd3882516874c86bc926726bc557d5184/kernel/packages/unity-interface/UnityScene.ts#L19) around the runtime scene  

### Kernel - Avatar Scene

It is a regular Decentraland [Scene](https://github.com/decentraland/explorer/blob/af59463dd3882516874c86bc926726bc557d5184/kernel/packages/ui/avatar/avatarSystem.ts), it has the size of the world. And it renders the avatars using the SDK

### Matrix Client 

The [Matrix Client](https://github.com/decentraland/matrix-client) can be used to interact Decentraland's users, providing the ability to send private messages and add people as friends.

### Sagas 

Like an ESB. Everything is connected to Sagas

### Synapse

[Synapse](https://matrix.org/docs/projects/server/synapse) server is an implementation of the [Matrix Protocol](https://matrix.org/), created for secure, decentralized communications. In the context of Decentraland it is used to manage private chats between peers and friendships. 

## Explorer Website

[REACT Application](https://github.com/decentraland/explorer-website) to load Kernel and Renderer

**Repositories**:
- Web Site https://github.com/decentraland/explorer-website
## Scene Runtime 

### Kernel - Runtime 

The [Runtime](https://github.com/decentraland/explorer/blob/df1d30412dcd1a94d933171a39796837aedc87a1/kernel/packages/scene-system/sdk/SceneRuntime.ts) handles SDK bindings and messaging with the Scene in Kernel

### Compiler Bundle 

#### AMD
This [Module](https://github.com/decentraland/js-sdk-toolchain/tree/c648dcabc0ac1aade3cf143769f7e7f67ffba95b/packages/%40dcl/amd) manages loading of RPC modules to interact with different components of Decentraland

**Repositories**
- https://github.com/decentraland/js-sdk-toolchain
#### ECS
The public library to interact with Decentraland. Sometimes people refers to the ECS as “The SDK”

#### User Code
The user generated code is part of the bundle of the Scenes


