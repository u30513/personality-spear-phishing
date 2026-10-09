<div align="center">

# Personality-Based System Against Spear-Phishing

**Using OSINT and Generative AI**

*An investigation into whether personality traits predict susceptibility to*
*personalised phishing attacks, and into the effect of adapting an attack to*
*the individual receiving it.*

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

A research platform developed to establish whether an individual's personality
predicts their response to a targeted phishing attempt, and to provide the
instrumentation required to examine that question under controlled conditions,
such that any resulting finding may be translated into defensive practice.

> This repository constitutes the public documentation of the project. The
> implementation is not publicly available; see
> [Why the source is private](#-why-the-source-is-private).

---

## 📌 The problem

Phishing constitutes one of the most prevalent and consistently effective
forms of cybercrime, affecting private individuals, commercial organisations
and public institutions alike. Estimates place worldwide annual losses in the
order of trillions of dollars. The resulting harm is not exclusively
financial: successful attacks may additionally produce the appropriation of
proprietary material, the disclosure of confidential records, the interruption
of operations, and a decline in institutional credibility.

Attack methodology has shifted substantially. Indiscriminate mass campaigns
have been progressively displaced by spear-phishing, in which messages are
composed for a specific individual or for a narrowly defined group. The
effectiveness of this approach derives from its use of contextual information.
Open-source intelligence techniques permit an attacker to assemble a profile
of the intended recipient from freely accessible material, and to construct an
approach aligned with that individual's apparent convictions, interests and
immediate circumstances.

Developments in generative AI have intensified this capability. Contemporary
language models generate fluent and contextually appropriate text on demand,
thereby removing the irregular phrasing and conspicuous errors that users have
conventionally been trained to recognise as indicators of fraud.
Personalisation that formerly required substantial manual effort for each
target may now be produced automatically and at scale, increasing both the
reach and the success rate of campaigns, while existing defences remain
calibrated against an earlier and less refined form of attack.

Current countermeasures demonstrate limited effectiveness. Recent evaluations
of awareness and training interventions report modest results, attributable
less to implementation than to design: such programmes typically issue uniform
guidance to all recipients and treat the population as homogeneous, thereby
neglecting the individual characteristics that determine why one recipient
acts upon a fraudulent message while another disregards it. The disparity
between the precision of contemporary attacks and the uniformity of the
countermeasures deployed against them represents a substantial weakness in
present-day security education.

Personality is among the characteristics in question, and its association with
phishing susceptibility has been established in the literature summarised
below. Few operational systems, however, incorporate personality into the
construction of the simulations employed for training purposes. The dimension
that research identifies as relevant consequently remains largely unexploited
in practice.

The present project addresses a narrower and empirically testable formulation
of the question:

> **Does an individual's personality profile predict their response to a
> spear-phishing attempt, and does adapting the pretext to that profile alter
> the outcome?**

The study accordingly examines the correlation between demographic variables,
Big Five personality traits as measured by the NEO PI-R, trait self-control,
and observed behaviour under controlled phishing simulation.

The implications are bidirectional, and they govern how the work is conducted.
Should personality prove a reliable predictor of susceptibility, training that
disregards it allocates equivalent effort to recipients of markedly unequal
exposure. The same personalisation that would render such training effective
would, however, equally render an attack effective. The generative component
of this project is restricted accordingly.

---

## 📚 Research lineage

The project continues an established line of research into the relationship
between phishing susceptibility and personality, published in peer-reviewed
journals and presented at conferences in the field.

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

López-Aguilar and Solanas (2021) reported the absence of a well-established
psychological theory accounting for the role of neuroticism in phishing
contexts, together with a lack of consensus across the literature, which the
authors attributed principally to non-representative samples and to
insufficient homogeneity between studies. López-Aguilar et al. (2022) applied
comparable systematic treatment to extraversion. López-Aguilar et al. (2025)
synthesised the field more broadly, reporting positive associations between
vulnerability and extraversion, agreeableness and neuroticism, with
conscientiousness functioning as a protective factor.

Systematic review, by its nature, cannot test the underlying mechanism
directly, nor can it measure the effect of deliberately adapting a pretext to
a given profile. The reviews establish association and identify the
methodological sources of disagreement within the field, namely inconsistent
samples and incomparable study designs. The present platform is constructed to
address the same question under the conditions those reviews identify as
absent, advancing it from documented association to controlled experimental
measurement.

---

## ⚙️ The three components

Each component addresses a distinct element of the measurement problem.

<br/>

### 🧩 Personality assessment framework

> **May a psychometric profile be obtained and scored reliably at the scale
> required by the study?**

The framework implements the complete lifecycle of a psychometric instrument:
ingestion of survey responses, cleaning and validation, scoring, and
generation of individual reports. Two instruments are currently implemented.

| Instrument | Measures |
|---|---|
| **NEO PI-R** (Costa & McCrae, 1992) | the Big Five across 30 facets |
| **Self-Control Scale** (Tangney et al., 2004) | a 36-item trait measure |

Participants receive their individual profile confidentially. Administration
is independent of the behavioural phase.

<br/>

### 🔤 Personality inference from text

> **May personality be inferred from written language alone?**

A requirement for full psychometric assessment of every subject imposes a
constraint that does not extend beyond the research setting, and to which an
attacker is not subject. This module trains models to predict NEO PI-R facet
scores directly from written language, in order to determine whether natural
text carries sufficient signal to approximate a profile. The question is of
independent research interest and additionally determines the realism of the
broader threat model.

A parallel line of enquiry examines whether self-regulation capacity may be
predicted from personality facets alone, using NEO PI-R scores as features.

<br/>

### 🎯 OSINT-informed pretext generation

> **Does a pretext adapted to the individual alter the outcome?**

The behavioural phase requires a pretext credible to a specific recipient.
This component combines a participant's personality profile with contextual
information derived through open-source intelligence in order to generate a
tailored simulation message. Safety constraints are embedded within the
generation step itself: output is framed as training material and must contain
no active links, no attachments and no request for sensitive data, with the
consequence that a generated message remains a simulation irrespective of how
the delivery platform is subsequently configured.

The **[prompt template](prompt_template.md)** is published here for purposes
of reproducibility. It represents the element of the method that may be
examined and evaluated without distribution of an operational capability,
specifying what is requested of the model and the constraints within which the
request is bounded. The surrounding apparatus is not published: open-source
intelligence collection, the binding of profile to prompt, and campaign
orchestration.

➡️ **[Read the prompt template](prompt_template.md)**

---

## 🧪 Study design

The design comprises two independent phases, structured such that no single
dataset associates an individual's personality profile with their phishing
outcome outside the research pipeline.

| | Phase 1 - self-report | Phase 2 - behavioural |
|---|---|---|
| **Instrument** | NEO PI-R and self-control measure | Personalised phishing simulation |
| **Delivery** | Online questionnaire | Phishing-simulation platform |
| **Disclosure** | Generic study aims only | Deception disclosed upon conclusion of participation |
| **Output** | Individual personality profile | One behavioural record per participant, per message |

The simulation platform is configured to record that a submission occurred
rather than its content, yielding a measure of susceptibility without the
study retaining participant credentials at any stage.

> **Ethics.** A favourable assessment was obtained from the university ethics
> committee prior to any data collection. Consent is obtained once, in
> advance, and covers both phases. All collection is conducted telematically;
> no in-person stage is involved. Advance disclosure of the phishing component
> would have invalidated the measurement, and post-participation debriefing
> therefore constitutes the mechanism by which the design remains both
> methodologically valid and ethically sound.

---

## 🔒 Why the source is private

- The apparatus surrounding the prompt constitutes, by construction, an
  operational method for converting a personality profile and publicly
  available information into a persuasive targeted pretext. The prompt design
  is published so that the method may be subject to review; the automated
  collection and orchestration that render it operational are not, the
  distinction between documenting a method and distributing it being material.
- Phase 2 records behaviour under a deception to which participants did not
  consent in advance. No derivative of that data may be made public,
  irrespective of consent obtained subsequently.
- Maintaining separation between the data and tooling of the two phases,
  including from public view, forms part of the validity argument rather than
  a precaution appended to it.

---

<div align="center">

**Research in progress.** The present document describes a methodology that
has received ethics approval. It does not report results, which are not yet
available.

</div>
