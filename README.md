<div align="center">
  <img src="assets/logo.png" alt="YOSO-YAi" width="160"/>
  <h1>mission-critical-discipline</h1>
  <h3>Engineering Posture for Infrastructure That Outlives Its Silicon</h3>
  <b>Build it once. Build it right. Build it to last three generations of compute.</b>

  <br/><br/>

  <img src="https://img.shields.io/badge/YOSO--YAi-mission--critical--discipline-C9A84C?style=for-the-badge&labelColor=0A0A0A"/>
  <img src="https://img.shields.io/badge/license-CC--BY--SA--4.0-C9A84C?style=for-the-badge&labelColor=0A0A0A"/>
  <img src="https://img.shields.io/badge/status-living--document-C9A84C?style=for-the-badge&labelColor=0A0A0A"/>
</div>

---

> The compute will go obsolete in five years. The infrastructure should not.

This repository captures the engineering discipline, field knowledge, and
professional conviction behind mission-critical electrical infrastructure.
It exists because the hyperscale data center industry has an incentive
problem: speed-to-power-on rewards cutting corners, and the planet pays for
it in landfill tonnage and embodied carbon. This repo documents the posture
that refuses to accept that trade-off. Sanitized of all client-specific
information.

---

## Table of Contents

1. [Why This Repo Exists](#1-why-this-repo-exists)
2. [What Mission Critical Means](#2-what-mission-critical-means)
3. [Power Distribution at Hyperscale](#3-power-distribution-at-hyperscale)
4. [The Foreman Seat](#4-the-foreman-seat)
5. [What the Industry Gets Wrong](#5-what-the-industry-gets-wrong)
6. [The Moral Case for Craftsmanship](#6-the-moral-case-for-craftsmanship)
7. [Patterns Observed](#7-patterns-observed)
8. [Repository Structure](#8-repository-structure)
9. [License](#9-license)

---

## 1. Why This Repo Exists

Francisco built his career across industrial electrical at Fluor Corporation
(conduit bending, journeyman-level craft), instrumentation and controls at
the Tesla Gigafactory (sensor integration, PLC logic), and electrical foreman
work at Meta NightCrawler (power distribution, data center wiring). Across
every rung, the same pattern repeated: schedule pressure erodes build quality,
and no one is held accountable for the infrastructure that ends up in a
landfill five years later.

This repository is a reference for anyone who believes infrastructure should
outlive the silicon it houses. It is sanitized of all client-specific
information.

---

## 2. What Mission Critical Means

The Uptime Institute defines four tiers of data center reliability. These are
public, industry-standard classifications:

| Tier     | Redundancy    | Expected Uptime | Concurrent Maintenance |
|----------|---------------|-----------------|------------------------|
| Tier I   | None (N)      | 99.671%         | No                     |
| Tier II  | Partial (N+1) | 99.741%         | No                     |
| Tier III | N+1           | 99.982%         | Yes                    |
| Tier IV  | 2N or 2N+1    | 99.995%         | Yes, fault tolerant    |

Mission-critical discipline means designing and building to Tier III or
Tier IV standards regardless of whether the customer procurement cycle
treats the building as disposable. The electrical craft does not change
because the buyer plans to throw the building away.

At Tier IV, every component in the power path has a parallel counterpart, and
every transfer between paths is automatic, tested, and verified. The facility
can sustain a fault without impact to the IT load. This level of redundancy
demands a corresponding level of craft in every termination, every conduit
run, every grounding connection.

---

## 3. Power Distribution at Hyperscale

A conceptual single-line diagram of utility-to-rack power distribution in a
hyperscale facility:

```
  UTILITY FEED(S)
       |
       |  (Redundant utility interconnects)
       v
  +----+----+       +----+----+
  | GEN SET |       | GEN SET |
  | BANK A  |  ...  | BANK N  |    Generator paralleling
  +----+----+       +----+----+    switchgear coordinates
       |                 |         multiple gen sets onto
       +--------+--------+         a common bus
                |
                v
       +--------+--------+
       | AUTO TRANSFER    |    ATS: senses utility loss,
       | SWITCH (ATS)     |    transfers to generator bus
       +--------+--------+
                |
                v
       +--------+--------+
       |   SWITCHGEAR     |    Main distribution, bus ties,
       |   (MAIN DIST)    |    protective relaying
       +--------+--------+
                |
         +------+------+
         |             |
         v             v
   +-----+-----+ +----+-----+
   |    UPS    | |    UPS    |    Uninterruptible power
   |  MODULE A | |  MODULE B |    supply: battery bridge
   +-----+-----+ +----+-----+    during transfer
         |             |
         +------+------+
                |
                v
       +--------+--------+
       |      PDU         |    Power distribution unit:
       | (Floor / Row)    |    transforms, monitors,
       +--------+--------+    distributes to racks
                |
         +------+------+
         |      |      |
         v      v      v
       RACK   RACK   RACK
```

Each layer introduces a transfer boundary. Mission-critical discipline means
every termination, every torque spec, every label at each boundary is
executed to craft standard, not to schedule standard.

Generator paralleling is a coordination problem: multiple diesel generators
synchronized on a common bus, sharing load proportionally, with protective
relaying to isolate a faulted unit without disturbing the bus. A failed
synchronization attempt (closing a breaker out of phase) is one of the most
dangerous events in the power system.

The UPS bridges the gap between utility failure and generator start. The ATS
transfers load from utility to generator. Hot aisle / cold aisle containment
separates intake and exhaust air to prevent recirculation and thermal
degradation.

---

## 4. The Foreman Seat

A foreman on a hyperscale electrical project holds the line between
engineering intent and field reality. The role includes:

- **Crew coordination** across multiple trades and shifts
- **Power distribution oversight** from switchgear through rack-level PDUs
- **Quality enforcement** on terminations, conduit runs, labeling, and testing
- **Schedule interface** between project management and craft labor
- **Safety authority** on the job site

Francisco held this seat at Meta NightCrawler, managing data center wiring
and power distribution with direct accountability for the quality of every
connection his crew made.

The foreman translates construction documents into installed, tested,
commissioned systems. The drawings say what to build. The foreman figures
out how to build it. That translation requires experience on both sides:
understanding the intent of the engineer and the reality of the field.

---

## 5. What the Industry Gets Wrong

The hyperscaler customer plans to demolish and rebuild every silicon cycle, so
their EPC builds for speed-to-power-on, not for longevity. Quality of build
collapses the moment the engineer understands the buyer plans to throw the
building away.

Francisco watched this firsthand at Tesla and Meta: rushed installations,
compromised craftsmanship, fragile systems shipped because the schedule was
the only thing that matters.

The infrastructure built that way ends up in landfills, the embodied carbon
wasted, the land scarred for nothing.

The gap between drawing quality and field execution widens under schedule
pressure. Engineering firms produce construction documents that are
technically correct but practically incomplete. The drawings show what to
build, not how to build it. The gap between "what" and "how" is filled by
the foreman and the crew, using experience, judgment, and craftsmanship. When
the schedule eliminates the time for that judgment, the gap fills with
defects.

---

## 6. The Moral Case for Craftsmanship

This is an environmental problem hiding inside a logistics problem.

When a facility is built to a five-year demolition horizon, every pound of
steel, every foot of copper, every yard of concrete carries embodied carbon
that gets written off at demolition. The Originator is engineered as
future-proof infrastructure. The envelope outlives three to four silicon
generations.

The discipline this repo documents is simple: build infrastructure that
survives the compute refresh cycle. If the envelope can house four generations
of silicon instead of one, the embodied carbon cost per compute-year drops
proportionally.

The crews who do this work deserve to build things that last. A journeyman
electrician who spends a full shift terminating heavy cable in a switchgear
lineup deserves to know that the work will stand for decades, not be
demolished before the warranty expires.

Craftsmanship is not nostalgia. It is carbon math.

---

## 7. Patterns Observed

General patterns observed across hyperscale electrical construction,
sanitized of all client-specific information:

| Pattern                          | Observation                                        |
|----------------------------------|----------------------------------------------------|
| Schedule-driven torque shortcuts | Terminations done to time, not to spec              |
| Label debt                       | Circuits left unlabeled under schedule pressure     |
| Hot aisle / cold aisle drift     | Containment breached for cable routing convenience  |
| Generator paralleling complexity | Multiple gen sets require precise relay coordination |
| UPS battery monitoring gaps      | Battery strings monitored at string level, not cell  |
| ATS transfer timing              | Transfer overlap windows tuned for speed, not clean  |
| Conduit fill violations          | Raceways overfilled to avoid pulling new conduit    |
| Drawing-to-field gap             | Construction documents incomplete for field reality  |

These are general industry patterns, not attributable to any specific client
or project. They are universal across hyperscale construction regardless of
operator, EPC, or geography.

---

## 8. Repository Structure

```
mission-critical-discipline/
  README.md
  LICENSE
  assets/
    logo.png
  docs/
    power-distribution.md
    tier-classifications.md
    foreman-role.md
    craftsmanship-thesis.md
    patterns-observed.md
```

---

## 9. License

This work is licensed under
[Creative Commons Attribution-ShareAlike 4.0 International (CC-BY-SA-4.0)](https://creativecommons.org/licenses/by-sa/4.0/).

You are free to share and adapt this material for any purpose, including
commercial, under the following terms:

- **Attribution** -- credit YOSO-YAi LLC and Francisco Montanez.
- **ShareAlike** -- distribute derivative works under the same license.

Sanitized of all client-specific information.
