# Architecture

## Overview

Campfire Tales is designed as a social platform for tabletop RPG campaigns, centered around shared knowledge, individual player perception, and campaign history.

The architecture is being defined during the project's early development phase. Technical choices may evolve as the domain model and product requirements become clearer.

## Core Concepts

The system is expected to represent several interconnected areas of a campaign:

* **Campaigns** — the main boundary for a group's RPG experience.
* **Characters** — player characters and other relevant entities in the campaign.
* **NPCs** — non-player characters and their relationships with the campaign.
* **Knowledge** — information known by the Game Master, the group, or individual players.
* **Relationships** — connections and perceived relationships between characters and entities.
* **Sessions** — individual game sessions and their resulting events.
* **Quests** — objectives, storylines, and related campaign activity.
* **Locations** — places that are part of the campaign world.
* **Events** — historical occurrences that contribute to the campaign's shared history.

These concepts are expected to evolve as the domain is explored further.

## Knowledge Model

A central architectural concern of Campfire Tales is that information is not necessarily equally available to every participant.

The campaign may contain information that is:

* Known by the Game Master.
* Shared with the entire group.
* Known by specific players.
* Inferred or perceived by individual characters.
* Hidden from players.

The system should therefore distinguish between the **state of the campaign world** and the **knowledge or perception of individual participants**.

The Game Master is responsible for controlling the authoritative campaign state and determining what information becomes available to players.

## Domain Boundaries

The campaign should act as the primary boundary for domain data.

Information belonging to one campaign should remain isolated from other campaigns unless an explicit sharing mechanism is introduced in the future.

Authentication, authorization, persistence, and presentation concerns should remain separate from the domain concepts wherever practical.

## Architectural Principles

### Domain-first design

The domain model should be driven by the needs of tabletop RPG campaigns rather than by the limitations of a particular technical implementation.

### Explicit information ownership

The system should make it possible to determine who owns, controls, or can access a piece of campaign information.

### Separation of world state and perception

The authoritative state of the campaign world should be distinguishable from what individual players know or believe about that world.

### Evolution over premature abstraction

The project is in an early stage. Architectural abstractions should be introduced when they solve demonstrated domain or technical problems rather than being created speculatively.

### Technology should support the domain

Technical decisions should serve the product and domain model. Frameworks, libraries, and infrastructure should not dictate domain concepts unnecessarily.

## Current State

The architecture is not considered final.

The following areas are still under discovery:

* Detailed domain model.
* Data ownership and visibility rules.
* User and campaign roles.
* Authentication and authorization.
* Persistence strategy.
* Application boundaries.
* API and communication patterns.
* Frontend architecture.
* Deployment and infrastructure.

Architecture documentation should be updated as these decisions become concrete.
