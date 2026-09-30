# 0001 — Domain Knowledge Model

* **Status:** Accepted
* **Date:** 2026-09-30

## Context

Campfire Tales represents RPG campaigns where the Game Master maintains the authoritative state of the campaign world while players progressively discover information about that world.

An entity may be known to the party while some of its properties remain unknown.

For example, players may know that an NPC named Eldrin exists without knowing his affiliation, motivations, or other private information.

The system therefore needs to distinguish between:

* What is true in the campaign world.
* Which entities the party has discovered.
* Which properties of those entities have been revealed.
* Comments and observations made by players.

## Decision

Campfire Tales will maintain a distinction between **canonical campaign state** and **party knowledge**.

### Canonical State

The canonical state represents the authoritative state of the campaign world and is controlled by the Game Master.

The GM is responsible for registering and maintaining this information in the application.

For example:

```text
NPC: Eldrin
Affiliation: Order of Ashes
Occupation: Merchant
```

The canonical value exists independently of whether the party knows it.

### Entity Discovery

Entities have their own discovery state.

A party may discover that an entity exists without knowing all of its details.

For example:

```text
Eldrin
Status: Discovered

Affiliation: Unknown
Occupation: Merchant
Motivation: Unknown
```

Entity discovery and field revelation are therefore separate concepts.

### Field Revelation

Individual fields may be revealed independently.

A field has a canonical value and a separate revelation state.

For example:

```text
Canonical:
Affiliation = Order of Ashes

Party:
Affiliation = Unknown
```

When the GM reveals the field:

```text
Party:
Affiliation = Order of Ashes
```

The canonical value is not changed by the revelation.

`Unknown` represents lack of knowledge, not the absence of a value.

### Party Knowledge

The initial model will use the **party as the knowledge boundary**.

The system does not currently model private knowledge for individual players.

A future decision may introduce individual knowledge if the product requires it.

### Player Comments

Players may add comments, observations, hypotheses, or notes about entities and their fields.

These comments are part of the party's recorded knowledge and perception and do not modify the canonical campaign state.

Comments remain available after the corresponding information is revealed.

For example:

```text
Affiliation: Order of Ashes

Comments:
- "He uses the same symbol as the Order."
- "He appears to know one of their members."
```

The comments preserve the history of the party's observations even after the underlying fact becomes known.

### Revelation

When the GM reveals information, the party's knowledge state changes without modifying the canonical state.

Revelation is currently treated as permanent within a campaign.

If the product later requires information to be hidden again, that behavior should be addressed by a separate architectural decision.

## Consequences

### Positive

* The authoritative campaign state remains separate from player knowledge.
* Entities can be discovered independently from their details.
* Individual fields can be revealed progressively.
* Player observations can be preserved independently of canonical information.
* The model supports mystery, investigation, and gradual discovery.

### Negative

* Canonical state and knowledge state must be represented separately.
* Visibility and revelation rules add complexity to the domain model.
* Future changes to knowledge boundaries may require additional modeling.

## Example

A newly discovered NPC may initially appear to the party as:

```text
Eldrin

Occupation: Merchant
Affiliation: Unknown
Motivation: Unknown
```

The GM's canonical state may be:

```text
Eldrin

Occupation: Merchant
Affiliation: Order of Ashes
Motivation: Protect the Order's interests
```

After the GM reveals the affiliation:

```text
Eldrin

Occupation: Merchant
Affiliation: Order of Ashes
Motivation: Unknown
```

The party now knows Eldrin's affiliation but still does not know his motivation.

## Future Considerations

The following concerns remain outside the scope of this decision:

* Individual player knowledge.
* Temporary or reversible revelations.
* Conflicting player perceptions.
* Historical changes to canonical values.
* Sharing or importing campaign content.
* Permissions and authorization mechanisms.
