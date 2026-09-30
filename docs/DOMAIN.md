# Domain

## Overview

Campfire Tales is centered around tabletop RPG campaigns and the information generated throughout their stories.

The domain model represents both the campaign world and the different ways users and participants interact with, understand, and remember that world.

The application also supports reusable campaign content through an optional content catalog and campaign templates. Entities may be reused without becoming part of the catalog, while cataloged entities can be explicitly made private or public.

The concepts described in this document are subject to change as the product and domain are explored further.

## Users

A **User** represents an authenticated person using Campfire Tales.

Users are application-level identities and are distinct from characters within a campaign.

Authentication is handled through an external authentication mechanism, initially using Google OAuth through NextAuth/Auth.js and its Prisma adapter.

Authentication-related entities such as accounts and sessions belong to the application infrastructure and are distinct from RPG campaign sessions.

A user may participate in multiple campaigns and may have different roles in each campaign.

A user may also own and manage reusable catalog content and campaign templates.

The same user may therefore be:

* A Game Master in one campaign.
* A Player in another campaign.
* A Game Master and Player across different campaigns.
* The owner of multiple campaign templates.
* The creator or owner of reusable content.

## Campaign Membership

A **Campaign Membership** represents the participation of a user in a campaign.

The user's role belongs to the membership rather than to the user itself, because a user may have different roles in different campaigns.

Initial campaign roles include:

* **Owner** — owns and manages the campaign.
* **Game Master** — manages the campaign and its world.
* **Player** — participates as a player in the campaign.

A campaign has a single owner, while multiple users may participate as Game Masters or Players.

For example, the same user may be:

* Owner and Game Master of Campaign A.
* Player of Campaign B.
* Game Master of Campaign C.

Campaign membership is also expected to become an important boundary for permissions, visibility, and knowledge access.

## Campaign

A **Campaign** represents an RPG campaign and acts as the primary boundary for its domain data.

A campaign contains its participants, characters, world information, events, sessions, quests, locations, relationships, and other related content.

Campaign data should remain isolated from other campaigns unless an explicit sharing or import mechanism is used.

A campaign has an owner and one or more members.

A campaign may be created:

* From scratch.
* From a campaign template.
* Through another future import or creation mechanism.

When content is imported into a campaign, the campaign receives its own instance of that content. Changes to that instance should not implicitly modify the source entity.

## Content Catalog

The **Content Catalog** is an optional mechanism for making entities reusable beyond their original context.

Any supported entity may be added to the catalog after it has been created, regardless of whether it was originally created inside a campaign, a template, or another supported context.

Cataloging an entity does not transfer ownership of the original entity and does not make the catalog entry a shared mutable instance.

A catalog entry preserves the reusable information and entity type necessary to create new instances of the content.

Catalog entries have an owner and a visibility setting.

Initial visibility options include:

* **Private** — only the owner can discover and reuse the catalog entry.
* **Public** — other users may discover and reuse the catalog entry.

A catalog entry may represent any supported reusable entity, such as:

* Characters and NPCs.
* Locations.
* Quests.
* Relationships.
* Factions or groups.
* Other campaign-world entities.

The exact set of catalog-supported entity types may evolve with the product.

### Importing Non-Cataloged Content

Content does not need to belong to the catalog to be reusable.

A user may import an entity from another context when the user has appropriate access to that source content.

For example, a user may create NPC John in Campaign B and later use John in Campaign C without adding John to the catalog.

The import creates a new instance in the destination context.

The source and destination entities have independent state after import.

### Cataloging Campaign Content

An entity created inside a campaign may later be added to the owner's catalog.

For example:

1. A user creates NPC John in Campaign B.
2. The user adds John to their catalog.
3. The user marks the catalog entry as private or public.
4. The catalog entry can then be reused in templates or other campaigns according to its visibility and access rules.

Adding an entity to the catalog does not alter the existing campaign instance.

Likewise, changes to a campaign instance do not automatically modify the catalog entry.

The exact rules for creating, updating, versioning, and promoting entities into the catalog remain subject to further domain exploration.

## Campaign Templates

A **Campaign Template** represents a reusable composition of campaign content intended to serve as a starting point for one or more campaigns.

A template may contain entities created specifically for the template as well as entities imported from other accessible contexts or from the content catalog.

Templates are intended to behave as reusable building blocks for campaign creation.

A template may contain:

* Characters and NPCs.
* Locations.
* Quests.
* Relationships.
* Events or other predefined campaign content.
* Other reusable world information.

A template has an owner and may be edited by users with appropriate permissions.

A template can be composed from reusable entities without requiring those entities to belong to the catalog.

For example:

1. A user creates Template A.
2. The user creates Template B.
3. The user creates NPC John while running Campaign B.
4. The user imports John into Template A without cataloging it.
5. Alternatively, the user adds John to the catalog and then imports the catalog entry into Template A.
6. Template A can subsequently be used to create new campaigns.

When a campaign is created from a template, the template's content is instantiated into the new campaign.

The resulting campaign owns its own state and can evolve independently.

Changes made to a campaign should not modify the template or source content from which it originated.

Likewise, modifying a template should not modify campaigns that were previously created from it.

## Characters

A **Character** represents an entity participating in or relevant to the campaign.

Characters may include:

* Player characters.
* Non-player characters.
* Other relevant entities within the campaign.

A character belongs to a campaign and therefore represents campaign-specific state.

A character may be associated with a user, but the user and character remain distinct concepts.

For example, a user may participate in a campaign as a Player and control one or more player characters.

The same user may control different characters in different campaigns.

A reusable character or NPC imported from another context becomes a campaign-specific character when instantiated into a campaign.

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

An NPC may be added to the content catalog and reused in multiple templates or campaigns.

Catalog reuse creates new instances rather than sharing mutable campaign state.

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

The relationship between users, characters, knowledge, and permissions remains subject to further domain exploration.

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

Relationships may be reused through the content catalog or campaign templates when appropriate.

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

A gameplay session is distinct from an authentication session managed by NextAuth/Auth.js.

## Quests

A **Quest** represents an objective, storyline, or ongoing activity within a campaign.

Quests may involve multiple characters, locations, events, and sessions.

Their state may change throughout the campaign as players interact with the world.

Quests may be created directly in a campaign, added to the content catalog, imported from another accessible context, or included in a campaign template.

## Locations

A **Location** represents a place within the campaign world.

Locations may be associated with:

* Characters.
* NPCs.
* Events.
* Quests.
* Sessions.
* Other locations.

Location information may also be subject to different visibility and knowledge rules.

Locations may be reused through the content catalog, imported from another accessible context, or included in a campaign template.

## Events

An **Event** represents something that happened within the campaign.

Events contribute to the historical record of the campaign and may be associated with a specific session, location, character, quest, or other domain concept.

An event may be:

* Known to the Game Master.
* Shared with the group.
* Known only by specific players.
* Unknown to some participants.
* Perceived differently by different characters.

Events are primarily campaign-specific because they contribute to the historical state of a particular campaign.

Whether all event types should be reusable through the content catalog or campaign templates remains subject to further domain exploration.

## World State and Perception

The domain distinguishes between two related concepts:

**World state** represents what is considered to have actually happened or currently exists within the campaign.

**Perception** represents what a particular participant or character believes, knows, or understands about that state.

These concepts do not necessarily have to agree.

For example, an NPC may secretly belong to a faction in the authoritative campaign state while a player believes the NPC is unaffiliated.

This distinction is fundamental to the domain and should be preserved as the model evolves.

## Content Reuse and Instantiation

Reusable content and campaign state are intentionally distinct.

The general lifecycle of reusable content is:

```text
Entity
  │
  ├── remains in its original context
  │
  ├── imported into another accessible context
  │
  └── optionally added to the Content Catalog
          │
          ├── Private
          │
          └── Public
```

Catalog entries and other importable content are sources for creating new instances.

When content is imported into a campaign or template, the destination receives its own instance.

For example:

```text
Campaign B
└── NPC John
      │
      ├── import ────────► Campaign C
      │                       └── NPC John
      │
      └── add to catalog
              │
              ├──► Template A
              ├──► Template B
              └──► Campaign D
```

The resulting instances have independent state.

The system should not implicitly synchronize changes between the source entity and imported instances.

Versioning, lineage, synchronization, inheritance, and update propagation remain subject to further domain exploration.

## Domain Evolution

The concepts described here are intentionally high-level.

The following aspects remain under discovery:

* Exact relationships between domain concepts.
* Campaign permissions and role capabilities.
* Ownership and sharing rules for catalog content.
* Catalog visibility and discovery rules.
* Exact rules for importing content between contexts.
* Which entity types can be cataloged.
* Which entity types can be imported.
* Difference between player and character knowledge.
* Visibility and access rules.
* Historical state and changes over time.
* Whether perceptions should be modeled independently from knowledge.
* Versioning of catalog content and campaign templates.
* Template composition and dependencies.
* Rules for promoting campaign content into the catalog.
* Whether public catalog content requires moderation or publication states.
* Whether templates can be shared or published independently from their contents.
* Synchronization or inheritance between reusable content and instantiated campaign content.
* Additional concepts required by the product.
