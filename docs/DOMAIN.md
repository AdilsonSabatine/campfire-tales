# Domain

## Overview

Campfire Tales is centered around tabletop RPG campaigns and the information generated throughout their stories.

The domain model represents both the campaign world and the different ways participants interact with, understand, and remember that world.

The concepts described in this document are subject to change as the product and domain are explored further.

## Campaign

A **Campaign** represents an RPG campaign and acts as the primary boundary for its domain data.

A campaign contains its participants, characters, world information, events, sessions, quests, locations, and other related content.

Campaign data should remain isolated from other campaigns unless an explicit sharing mechanism is introduced.

## Characters

A **Character** represents an entity participating in or relevant to the campaign.

Characters may include:

* Player characters.
* Non-player characters.
* Other relevant entities within the campaign.

The distinction between player characters and NPCs may have different implications for permissions, ownership, and information visibility.

## NPCs

An **NPC** is a non-player character belonging to the campaign world.

NPCs may be associated with:

* Other characters.
* Locations.
* Events.
* Quests.
* Factions or groups.
* Player perceptions.

NPC information may contain both authoritative campaign information and information that is only known or perceived by specific players.

## Knowledge

**Knowledge** represents information about the campaign that is available to one or more participants.

Knowledge may have different scopes, including:

* Game Master knowledge.
* Shared group knowledge.
* Individual player knowledge.
* Character knowledge or perception.
* Hidden information.

Knowledge is distinct from the underlying state of the campaign world.

A fact may exist in the authoritative campaign state without being known to a particular player.

## Relationships

A **Relationship** represents a connection between entities within the campaign.

Relationships may describe connections such as:

* Friendship.
* Rivalry.
* Allegiance.
* Family.
* Trust.
* Hostility.
* Other campaign-specific connections.

A relationship may have an authoritative state while individual characters or players may hold different perceptions of that relationship.

## Sessions

A **Session** represents a specific gameplay session within a campaign.

Sessions provide a temporal context for events, discoveries, interactions, and changes to the campaign world.

A session may be associated with:

* Events.
* Characters.
* Quests.
* Locations.
* Knowledge changes.
* Other campaign activity.

## Quests

A **Quest** represents an objective, storyline, or ongoing activity within a campaign.

Quests may involve multiple cha
