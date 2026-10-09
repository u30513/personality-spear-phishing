<div align="center">

# Personality-Based System Against Spear-Phishing

**Using OSINT and Generative AI**

*Does personality predict who falls for a targeted phishing attack,*
*and what changes when the attack is written for them?*

<br/>

![Status](https://img.shields.io/badge/status-research%20in%20progress-2E7D86?style=flat-square)
![Ethics](https://img.shields.io/badge/ethics-committee%20approved-3F7D20?style=flat-square)
![Source](https://img.shields.io/badge/source-private-6E8492?style=flat-square)

![Python](https://img.shields.io/badge/Python-3.12-3776AB?style=flat-square&logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-F7931E?style=flat-square&logo=scikit-learn&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-ML-EC6C27?style=flat-square)
![Qualtrics](https://img.shields.io/badge/Qualtrics-API-00BF6F?style=flat-square)

</div>

---

A research platform that measures whether a person's personality predicts how
they respond to a targeted phishing attempt, and builds the tooling needed to
test that at scale, so the finding can be turned into defence rather than left
as intuition.

> This repository is the public write-up. The implementation is private; see
> [Why the source is private](#-why-the-source-is-private).

---

## 📌 The problem

Phishing remains among the most prevalent and reliably successful categories
of cybercrime, reaching private individuals, companies and public institutions
without distinction. Worldwide annual losses are estimated in the trillions of
dollars, and the harm extends well past the balance sheet: stolen proprietary
work, exposure of records that were meant to stay confidential, interrupted
operations, and the slow erosion of institutional credibility that follows a
publicised breach.

What has changed is precision. Indiscriminate bulk mailings have given way to
messages composed for one recipient, or for a narrowly drawn group. Their
potency comes from context. Using open-source intelligence, an attacker
assembles a picture of a target from material that is freely available, then
writes an approach that fits what that person values, worries about, or
happens to be dealing with that week. The message does not have to be
universally plausible. It only has to be plausible to one reader.

Generative AI has sharpened this considerably. Models now produce fluent,
situationally aware prose on demand, stripping away the awkward phrasing and
visible errors that users were taught to treat as warning signs. Tailoring
that previously cost an attacker real effort per target can be produced
automatically and in volume, lifting both the reach and the hit rate of a
campaign while defences remain calibrated against an earlier, cruder form of
the attack.

Those defences are not holding. Recent evaluations of awareness and training
programmes report limited effect, and the reason is structural rather than
incidental: such programmes issue the same general guidance to everyone and
treat each recipient as interchangeable, leaving untouched the human
characteristics that determine why one person acts on a message and the next
deletes it. The distance between how precisely attacks are now aimed and how
uniformly countermeasures are delivered is among the weakest points in
current security education.

Personality is one of those characteristics, and its association with
susceptibility is established in the literature set out below. Yet almost no
working system carries personality into the construction of the simulations
used for training. The dimension the research identifies as relevant is
precisely the one practical tools leave out.

This project asks a sharper, testable version of the question:

> **Does a person's personality profile predict how they respond to a
> spear-phishing attempt, and does tailoring the pretext to that profile
> change the outcome?**

Specifically, it studies the correlation between demographic variables,
Big Five personality traits (NEO PI-R), trait self-control, and observed
behaviour under a controlled phishing simulation.

The answer cuts both ways, which shapes how the work is handled. If
personality measurably predicts susceptibility, training that ignores it is
spending the same effort on everyone regardless of exposure. But the
personalisation that makes such training effective is the same
personalisation that makes an attack effective, which is why the generation
side of this project is held closely rather than published.

---

## 📚 Research lineage

This is not a standalone project. It continues an established line of research
into the relationship between phishing susceptibility and personality,
published in peer-reviewed journals and presented at conferences in the field.

**López-Aguilar, P., Urruela, C., Batista, E., Machin, J., & Solanas, A.
(2025).** Phishing vulnerability and personality traits: Insights from a
systematic review. *Computers in Human Behavior Reports*, 20, 100784.
[![DOI](https://img.shields.io/badge/DOI-10.1016%2Fj.chbr.2025.100784-004E89?style=flat-square)](https://doi.org/10.1016/j.chbr.2025.100784)

**López-Aguilar, P., Patsakis, C., & Solanas, A. (2022).** The role of
extraversion in phishing victimisation: A systematic literature review.
*2022 APWG Symposium on Electronic Crime Research (eCrime)*.
[![DOI](https://img.shields.io/badge/DOI-10.1109%2FeCrime57793.2022.10142078-004E89?style=flat-square)](https://doi.org/10.1109/eCrime57793.2022.10142078)

**López-Aguilar, P., & Solanas, A. (2021).** Human susceptibility to phishing
attacks based on personality traits: The role of neuroticism. *2021 IEEE 45th
Annual Computers, Software, and Applications Conference (COMPSAC)*.
[![DOI](https://img.shields.io/badge/DOI-10.1109%2FCOMPSAC51774.2021.00192-004E89?style=flat-square)](https://doi.org/10.1109/COMPSAC51774.2021.00192)

López-Aguilar and Solanas (2021) found no well-established psychological theory
accounting for the role of neuroticism in phishing, and no unanimity across the
literature, attributing the disagreement largely to non-representative samples
and a lack of homogeneity between studies. López-Aguilar et al. (2022) applied
the same systematic treatment to extraversion. López-Aguilar et al. (2025)
synthesised the field more broadly, reporting extraversion, agreeableness and
neuroticism as positively associated with vulnerability, with
conscientiousness acting as a protective factor.

What none of that can do, by the nature of a systematic review, is test the
mechanism directly or measure what happens when a pretext is deliberately
tailored to a profile. The reviews establish association and expose exactly
why the field disagrees: inconsistent samples and incomparable study designs.
This platform is built to answer the same question under conditions the
reviews identified as missing, moving it from reviewed association to
controlled, instrumented experiment.

---

## 🔬 The pipeline

```mermaid
flowchart LR
  subgraph PH1["PHASE 1 - Self-report"]
    A["NEO PI-R<br/>Big Five, 30 facets"]
    B["Self-Control Scale<br/>36 items"]
  end

  subgraph GEN["Generation - not published"]
    O["OSINT context"]
    T["Prompt template<br/>safety-constrained"]
  end

  subgraph PH2["PHASE 2 - Behavioural"]
    S["Simulation platform"]
    R["Behavioural record<br/>submission: yes / no"]
  end

  A --> P["Personality profile"]
  B --> P
  P --> T
  O --> T
  T --> M["Personalised message"]
  M --> S
  S --> R
  P --> AN["Analysis<br/>traits vs. susceptibility"]
  R --> AN
```

The two phases never meet except at the analysis step. That separation is the
design, not an implementation detail.

---

## ⚙️ The three components

Each solves a different part of the measurement problem.

<br/>

### 🧩 Personality assessment framework

> **Can a psychometric profile be collected and scored reliably at study
> scale?**

A reusable pipeline covering the full lifecycle of a psychometric instrument:
ingesting survey responses, cleaning and validating them, scoring, and
generating individual reports. Two instruments are implemented:

| Instrument | Measures |
|---|---|
| **NEO PI-R** (Costa & McCrae, 1992) | the Big Five across 30 facets |
| **Self-Control Scale** (Tangney et al., 2004) | a 36-item trait measure |

Participants receive their own profile back confidentially; the instrument is
administered independently of the behavioural phase.

<br/>

### 🔤 Personality inference from text

> **Can personality be inferred from written language alone?**

If a full psychometric instrument is required for every subject, the method
does not scale beyond a study, and an attacker certainly is not sending
questionnaires. This module trains models to predict NEO PI-R facet scores
**directly from written language**, testing whether natural text carries
enough signal to approximate a profile. It is both a research question in its
own right and the component that determines whether the broader threat model
is realistic.

A parallel line of work asks whether self-regulation capacity can be predicted
from personality facets alone, using NEO PI-R scores as features.

<br/>

### 🎯 OSINT-informed pretext generation

> **Does a pretext written for the person change the outcome?**

The behavioural phase requires a lure that is credible to a specific person.
This component combines a participant's personality profile with
OSINT-derived personal and professional context to generate a tailored
simulation message. Safety constraints are built into the generation step
itself: output is framed as training material and must contain no active
links, no attachments, and no request for sensitive data, so a generated
message remains a simulation independently of how the delivery platform is
configured.

The **[prompt template](prompt_template.md)** is published here for
reproducibility. It is the part of the method that can be examined and
critiqued without handing over a working capability: what gets asked for, and
the constraints the request is bounded by. What is not published is everything
around it, namely the OSINT collection, the binding of a profile to a prompt,
and the campaign orchestration.

➡️ **[Read the prompt template](prompt_template.md)**

---

## 🧪 Study design

Two deliberately independent phases, so that no single dataset links a
person's personality profile to their phishing outcome outside the research
pipeline.

| | Phase 1 - self-report | Phase 2 - behavioural |
|---|---|---|
| **What** | NEO PI-R + self-control instrument | Personalised phishing simulation |
| **Delivery** | Online questionnaire | Phishing-simulation platform |
| **Disclosure** | Generic study aims only | Deception disclosed after participation ends |
| **Output** | Individual personality profile | One behavioural record per participant, per message |

The simulation platform is configured to record **that** a submission
occurred, not **what** was submitted, yielding a susceptibility measure
without the study ever holding a participant credential.

> **Ethics.** Favourable assessment from the university ethics committee
> preceded any data collection. Consent is collected once, up front, covering
> both phases. All collection is telematic; there is no in-person stage.
> Disclosing the phishing component in advance would have destroyed the
> measurement, which is why the post-participation debrief, rather than an
> upfront warning, is the mechanism that keeps the design both valid and
> ethical.

---

## 🔒 Why the source is private

- The pipeline around the prompt is, by construction, a working method for
  turning a personality profile plus public information about a person into a
  convincing targeted pretext. The prompt design is published so the method
  can be reviewed; the automated collection and orchestration that make it
  operational are not, because describing a method is research and shipping
  it is distribution.
- Phase 2 records behaviour under a deception participants did not consent to
  in advance. Nothing derived from it can be public, regardless of consent
  obtained afterwards.
- Keeping the two phases' data and tooling separated, including from public
  view, is part of what makes the validity argument hold, not a precaution
  added on top of it.

---

<div align="center">

**Research in progress.** This describes a methodology that has cleared ethics
review, not results, which do not yet exist.

</div>
