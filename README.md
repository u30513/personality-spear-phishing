<div align="center">

# Personality-Based System Against Spear-Phishing

**Using OSINT and Generative AI**

*Does personality predict susceptibility to personalised phishing,*
*and does adapting the attack to the individual alter the outcome?*

<br/>

![Ethics](https://img.shields.io/badge/ethics-committee%20approved-3F7D20?style=flat-square)

![Python](https://img.shields.io/badge/Python-3.12-3776AB?style=flat-square&logo=python&logoColor=white)
![BERT](https://img.shields.io/badge/BERT-embeddings-5C2D91?style=flat-square)
![scikit-learn](https://img.shields.io/badge/scikit--learn-MLP-F7931E?style=flat-square&logo=scikit-learn&logoColor=white)
![OpenAI](https://img.shields.io/badge/OpenAI-API-412991?style=flat-square&logo=openai&logoColor=white)
![Qualtrics](https://img.shields.io/badge/Qualtrics-API-00BF6F?style=flat-square)

</div>

---

> Public documentation of the project. The code is
> [available upon request](#-availability).

## 📌 The problem

Phishing remains among the most prevalent and effective forms of cybercrime,
with worldwide annual losses estimated in the trillions of dollars. Beyond
direct financial damage, successful attacks produce the appropriation of
proprietary material, the disclosure of confidential records, operational
disruption and lasting reputational harm.

Indiscriminate mass campaigns have been displaced by spear-phishing, in which
messages are composed for a specific individual. Open-source intelligence
allows an attacker to profile a target from freely accessible material and
construct an approach aligned with their interests and circumstances.
Generative AI has intensified this capability: language models produce fluent,
contextually appropriate text on demand, removing the irregular phrasing users
are trained to recognise, and rendering per-target personalisation automatic
and scalable.

Defences have not kept pace. Recent evaluations of awareness training report
modest effect, attributable to design rather than implementation: such
programmes issue uniform guidance and treat the population as homogeneous,
neglecting the individual characteristics that determine why one recipient
acts upon a fraudulent message and another disregards it. Personality is among
those characteristics, its association with susceptibility established in the
literature below, yet few operational systems incorporate it into the
simulations used for training.

> **Does an individual's personality profile predict their response to a
> spear-phishing attempt, and does adapting the pretext to that profile alter
> the outcome?**

The study examines the correlation between demographic variables, Big Five
personality traits, trait self-control and observed behaviour under controlled
simulation. The same personalisation that would make such training effective
would equally serve an attack, and access to the generative component is
controlled accordingly.

---

## 📚 Research lineage

The project continues an established line of research, published in
peer-reviewed journals and presented at conferences in the field.

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

The 2021 study reported no well-established theory accounting for neuroticism
in phishing contexts and no consensus across the literature, attributing the
disagreement to non-representative samples and insufficient homogeneity
between studies. The 2022 review applied comparable treatment to extraversion.
The 2025 synthesis reported positive associations between vulnerability and
extraversion, agreeableness and neuroticism, with conscientiousness
functioning as a protective factor. Systematic review cannot test the
mechanism directly, nor measure the effect of deliberately adapting a pretext
to a profile; this platform addresses the same question under the conditions
those reviews identify as absent.

---

## 🧩 Proof of concept

A platform operationalising contextual and psychological profiling for
phishing simulation: it collects public information through open-source
intelligence, constructs a Big Five profile, and generates an adapted
spear-phishing email. Three interdependent modules.

### 🔍 1. Open-source intelligence

> **Assemble the publicly available material associated with a target
> identity.**

Sixteen tools, each categorised by the identifier it accepts: email address,
pseudonyms, personal names, institutional domains. Collected text, including
opinions and activity on social networks, is exported in tabular form for the
next stage.

### 🧠 2. Personality analysis

> **Convert the collected text into a Big Five profile.**

Only sentences authored by the target are retained. These are converted into
vector embeddings using a pre-trained BERT model, enriched with
psycholinguistic features, and supplied to a multilayer perceptron trained to
predict Big Five scores. Each comment is scored individually, then aggregated
into an overall profile expressed as means between 0 and 1.

The approach draws on established association rules: frequent positive emotion
correlates with extraversion, cautious or highly structured phrasing with
conscientiousness. Each trait is treated as an explicit, interpretable signal
feeding the generation instructions. The result indicates disposition
sufficient to inform adaptation; it is not a clinical assessment.

### ✉️ 3. Spear-phishing generation

> **Produce a message adapted to the profile and the context.**

The module combines the profile with context gathered during the OSINT phase,
such as employment, institution and identified interests, on the hypothesis
that success depends substantially on the recipient's personality and on
adapting tone, style and content to their expected behaviour.

| Elevated trait | Adaptation applied to the message |
|---|---|
| **Openness** | emphasis upon novelty and innovation |
| **Conscientiousness** | professional and well-structured tone |
| **Extraversion** | socially engaging content, energetic tone, opportunity for interaction |
| **Agreeableness** | empathetic and cooperative language, emphasising harmony and concern for others |
| **Neuroticism** | conveyed urgency and the salience of potential risk |

Scores and context are translated into a structured prompt. The implementation
uses the OpenAI API but is model-agnostic. Safety constraints are embedded in
the generation step: output is framed as training material and must contain no
active links, no attachments and no request for sensitive data, so a generated
message remains a simulation regardless of how the delivery platform is
configured.

➡️ **[Read the prompt template](prompt_template.md)**

---

## 🧪 Study design

Two independent phases, structured so that no single dataset associates a
personality profile with a phishing outcome outside the research pipeline.

| | Phase 1 - self-report | Phase 2 - behavioural |
|---|---|---|
| **Instrument** | NEO PI-R and self-control measure | Personalised phishing simulation |
| **Delivery** | Online questionnaire | Phishing-simulation platform |
| **Disclosure** | Generic study aims only | Deception disclosed upon conclusion |
| **Output** | Individual personality profile | One behavioural record per participant, per message |

Phase 1 establishes a measured profile against which inferred profiles and
observed behaviour are compared, using the NEO PI-R (Costa & McCrae, 1992),
covering the Big Five across 30 facets, and the Self-Control Scale (Tangney et
al., 2004), a 36-item trait measure. Participants receive their profile
confidentially. The simulation platform records that a submission occurred
rather than its content, yielding a susceptibility measure without the study
holding participant credentials.

> **Ethics.** Favourable assessment from the university ethics committee
> preceded data collection. Consent is obtained once, in advance, covering
> both phases; all collection is telematic. Advance disclosure of the phishing
> component would have invalidated the measurement, and post-participation
> debriefing is therefore the mechanism by which the design remains both valid
> and ethical.

---

## 🔒 Availability

**The implementation is available upon request**, for research, peer review
and replication. Requests may be directed to the repository owner.

It is not published openly because the apparatus surrounding the prompt
constitutes an operational method for converting a personality profile and
publicly available information into a persuasive targeted pretext, and open
distribution would place that capability in general circulation. Participant
data from Phase 2 is not shareable in any form, independently of the status of
the code.
