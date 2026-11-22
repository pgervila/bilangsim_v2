# Society domains

> **Status:** draft v0 (Nov 2026), for discussion. This document defines the
> spheres of social life the model represents: who meets whom, how often, which
> words they use, which language they choose, and which policies act there. It
> keeps the legacy model's domains
> ([`background/modeling_solutions/legacy_best_ideas.md`](background/modeling_solutions/legacy_best_ideas.md))
> and adds the ones it lacked. Uncertain facts about data sources are marked
> *(to check)*.
>
> **Generic first (DEC-08).** The domains are defined for a generic bilingual
> society with languages **A** and **B** (DEC-07). In v1, their parameters
> (time per domain, group sizes, norms) are set within plausible ranges from
> the literature. The data sources named below, mostly Catalan (census,
> EULP), are for the later **specific-society phase**. Catalan examples
> illustrate the mechanisms; they are not built in.

---

## 0. Summary

| Code | Domain | In legacy? | v1? | Main language-choice mechanism | Main policy lever | Data (specific-society phase) |
|---|---|---|---|---|---|---|
| **HOME** | Home and family, including extended family | yes | yes | memory of the language used with each relative; the parents' transmission decision | (indirect: awareness campaigns) | EULP: language with parents, partner, children |
| **CARE** | Early childhood care (0–3 years) | yes (daycare from 1 year) | yes | the institution's language; the carer's language | language of public childcare | enrolment rates by age; childcare language *(to check)* |
| **SCHOOL** | School, 3–18 years: classroom, peers, playground, school gate | yes | yes | in class: policy; out of class: peer norms (MAXIMIN plus relationship memory) | **hours of instruction per language per grade** | curriculum regulations; school surveys of language use *(to check)*; census knowledge by age |
| **UNIV** | Higher education | yes | yes (simple) | institution's language plus peer norms | language of instruction | enrolment; university language statistics *(to check)* |
| **WORK** | Work: colleagues, internal norms | yes | yes | the workplace's internal norm; requirement for hiring; colleagues' relationship memory | **language requirements by sector** | EULP: language at work; labour-force survey (sectors) |
| **SERV** | Services and commerce: shops, bars, banks; encounters between provider and client | partly (customers) | yes | the initiator's choice and the **accommodation norm**; the provider's obligations | consumer language rights; labelling and service obligations | EULP: language in shops, large stores, banks *(to check)* |
| **ADMIN** | Public administration and public services, including health | no | v2 | institutional default plus the citizen's choice | language of public services | EULP: language with doctors and administration *(to check)* |
| **SOCIAL** | Friends and leisure: friendship networks, associations, sports | yes (friends) | yes | relationship memory; homophily | (support for associations) | EULP: language with friends |
| **PUBLIC** | Neighbourhood and public space: neighbours, strangers, overheard speech | yes (bystanders) | yes (simple) | MAXIMIN with perceived profiles; overhearing | — | EULP: language with neighbours, with strangers *(to check)* |
| **MEDIA** | Media and digital: TV, radio, streaming, press, social media, games | sketched | yes (exogenous input) | the offer per language × individual preference | **media offer and quotas; public broadcaster** | media audiences by language *(to check)* |

---

## 1. Concepts

| Term | Meaning | Example |
|---|---|---|
| **Domain** | A sphere of life with its own participants, purposes and norms of language use (Fishman, 1972) | WORK |
| **Setting** | A concrete instance of a domain: a place, a group, a time pattern | "class 3B of school 12, weekdays 9:00–16:30" |
| **Activity** | What people do in a setting, with an interaction structure | a teacher addressing the class; a pair chatting at break |
| **Event** | One timestamped occurrence of an activity, with its participants. This is what the learning core receives. | 14 Mar 2031, class 3B, teacher → 24 pupils, Catalan, 6,000 words |
| **Register** | The word distribution used in an activity (F1, F3) | child-directed, school-academic, work by sector, conversational, media |
| **Norm** | How a setting constrains the choice of language | institutional policy; accommodation; the language a pair has always used |

**Why domains matter for the research question.**
- Languages are kept and lost domain by domain, with the minority language
  typically retreating to the home (Fishman, 1991).
- Vocabulary is domain-specific. Bilingual children's receptive-vocabulary gap
  is concentrated in home words, not school words (Bialystok et al., 2010).
- Policies act on specific domains.

So the model must represent domains separately, both for *language choice* and
for *vocabulary*.

---

## 2. Which domains each life stage takes part in

● main domain, ○ minor, – none.

| Domain | Infant 0–3 | Child 3–12 | Adolescent 12–18 | Young adult 18–30 | Adult 30–65 | Older adult 65+ |
|---|---|---|---|---|---|---|
| HOME | ● | ● | ● | ● | ● | ● |
| CARE | ● (if enrolled) | – | – | ○ (as parent) | ○ (as parent) | ○ (as grandparent) |
| SCHOOL | – | ● | ● | ○ (as parent) | ○ (as parent) | – |
| UNIV | – | – | – | ● (if student) | – | – |
| WORK | – | – | ○ (part-time) | ● | ● | – |
| SERV | ○ (with parents) | ○ | ○ | ● | ● | ● |
| ADMIN (v2) | ○ (health) | ○ (health) | ○ | ○ | ○ | ● (health) |
| SOCIAL | – | ○ | ● | ● | ○ | ○ |
| PUBLIC | ○ (overheard) | ○ | ○ | ○ | ○ | ○ |
| MEDIA | ○ | ● | ● | ● | ● | ● |

Time per domain and life stage is calibrated on time-use surveys. Words heard
and spoken per hour are calibrated on daylong recordings (Mehl et al., 2007;
LENA norms for children).

---

## 3. The domains

Each domain is described with the same fields:
- participants;
- interaction structure;
- register;
- language choice;
- policy levers;
- what legacy had;
- calibration data;
- v1 scope.

### 3.1 HOME — home and family

- **Participants.** The household (couple, children, sometimes grandparents)
  and the extended family (grandparents, uncles and aunts, cousins), with
  typed and reciprocal kinship.
- **Interaction.**
  - Daily household talk.
  - Child-directed speech to infants and children.
  - Overheard adult talk.
  - Visits and gatherings of the extended family, often led by grandparents.
  - Speech directed to a child predicts vocabulary better than overheard
    speech (Weisleder & Fernald, 2013), so the two are tracked separately.
- **Register.** Child-directed (CHILDES) for young children; home and
  conversational vocabulary otherwise.
- **Language choice.**
  - **The couple's language** is set when the couple forms (their
    acquaintance language) and sticks.
  - **The language with a newborn** is each parent's **transmission
    decision**, driven by three motives: proficiency, perceived status and
    defence against assimilation. It is constrained by the couple's language
    and the child's expected environment
    ([`specs/motives_and_transmission.md`](specs/motives_and_transmission.md)).
  - **Relatives** follow the linking parent's language with the child if they
    speak it well enough.
  - **Siblings** settle on a language between themselves, possibly drifting
    toward the school or peer language *(target to check)*.
  - Every dyad's language can be **renegotiated** when proficiency changes.
- **Policy levers.** Indirect only: campaigns, support for parents.
- **From legacy.** Transmission choice, the family following it, typed
  kinship, gatherings led by the elderly (legacy ideas §4).
- **Calibration data.** EULP: language with mother, father, partner and
  children. These give intergenerational transmission rates by couple type.
  Census: household composition.
- **v1:** all of the above. Transmission is the most important decision in the
  model.

### 3.2 CARE — early childhood care (0–3)

- **Participants.** Infants, carers, and parents at drop-off and pick-up.
- **Interaction.** Carers' speech directed to the group and to single
  children; peers; parents talking with carers and with each other.
- **Register.** Child-directed.
- **Language choice.** The institution's language for carers. Parents and
  carers use MAXIMIN and their relationship memory.
- **Policy levers.** The language of public childcare.
- **From legacy.** Daycare from 1 year; the meeting point between parents and
  teachers (legacy ideas §7). The legacy "no input before 1 year" gate is
  removed.
- **Calibration data.** Enrolment rates by age; the language of childcare
  *(to check)*.
- **v1:** yes, simple.

### 3.3 SCHOOL — schooling from 3 to 18

- **Participants.** Pupils in classes by grade, teachers, other staff, and
  parents at the school gate.
- **Interaction.**
  - Instruction: the teacher addresses the class, which is directed speech.
  - Pair and group work.
  - Breaks and playground with peers of nearby grades.
  - Parents' meetings at the gate.
  - Homework and reading (literacy, v2).
- **Register.** Academic, by grade and subject; peer conversation.
- **Language choice.**
  - **In class:** the language of instruction follows the **policy**:
    hours per language per grade and subject. The teacher speaks the policy
    language (the legacy hard-coded L1, legacy ideas §12).
  - **Outside class:** peer norms. MAXIMIN applies among classmates, plus the
    language each pair has always used.
  - The language of the playground can differ from the language of
    instruction *(target to check in school language surveys)*.
- **Policy levers.**
  - Hours per language per grade (immersion, conjunction, separate tracks).
  - Teachers' language requirements.
  - Reception classes for newcomers.
- **Staffing.** A policy needs teachers who can teach in its language. The
  supply of teachers is a constraint, and a shortfall is reported as an output
  (legacy ideas §7).
- **From legacy.** Courses by age, yearly promotion, teacher hiring and
  turnover, the policy as allowed teacher profiles, study time by policy.
- **Calibration data.**
  - Curriculum regulations (hours per language).
  - Census knowledge by age, which shows the cohort effect of schooling.
  - School surveys of language use *(to check)*.
- **v1:** yes. This is one of the two policy levers of v1.

### 3.4 UNIV — higher education

- **Participants.** Students by faculty and year, and lecturers.
- **Interaction.** Lectures (directed), peers, shared flats for students who
  move.
- **Register.** Academic.
- **Language choice.** The institution's language for lectures, plus peer
  norms.
- **Policy levers.** Language of instruction.
- **From legacy.** Universities in about 20 % of towns; students moving to
  university towns; faculties.
- **Calibration data.** Enrolment; share of teaching per language *(to
  check)*.
- **v1:** simple (attendance, peers, lecture language).

### 3.5 WORK — work

- **Participants.** Colleagues in a workplace, characterised by sector, size
  and clientele.
- **Interaction.**
  - Colleagues in groups and pairs.
  - Meetings.
  - Encounters with clients belong to SERV (seen from the client's side) and
    to WORK (seen from the worker's side).
- **Register.** Work vocabulary by sector, plus conversation.
- **Language choice.**
  - Each workplace has an **internal norm**, set by sector and by its
    workforce and clientele.
  - Colleagues use their relationship memory.
  - The legacy rule derived language requirements from the composition of the
    town, which is a good default to calibrate.
- **Policy levers.**
  - **Language requirements by sector**, e.g. public-facing jobs and the
    public sector.
  - Workplace training.
- **Hiring.** Requirements filter candidates. A rejection is an experience of
  exclusion (§4.4).
- **From legacy.** Requirements from local demography; hiring tied to
  language; job search biased to the local area with family constraints;
  links between workplaces (legacy ideas §7).
- **Calibration data.** EULP: language at work. Labour-force survey: sectors
  and employment by area *(to check access)*.
- **v1:** yes. This is the second policy lever of v1.

### 3.6 SERV — services and commerce

- **Participants.** Provider (a worker) and client, in shops, bars and
  restaurants, banks and other services.
- **Interaction.** Short encounters between strangers or semi-strangers, often
  repeated with the same shopkeeper.
- **Register.** Transactional.
- **Language choice.**
  - The **initiator** chooses, using a **perceived profile** of the other
    person (§4.2).
  - Accommodation follows. In general, speakers of the lower-status language
    converge more (Communication Accommodation Theory; Giles, Coupland &
    Coupland, 1991). In the model this is the status term of the choice
    (motives spec §6). Catalonia's **accommodation norm**, Catalan speakers
    switching to Spanish with people they take to be Spanish speakers
    (Woolard, 1989), is one case of it. Speakers with strong attachment and a
    perceived threat may refuse to accommodate.
  - Repeated encounters build relationship memory.
  - Providers may face service obligations.
- **Policy levers.** Consumer language rights; obligations to serve customers
  in a language; labelling.
- **From legacy.** Customer encounters across workplaces (legacy ideas §5.1).
- **Calibration data.** EULP: language in small shops, large stores and banks,
  and the language used to address strangers *(items to check)*.
- **v1:** yes. Short encounters are where accommodation is most visible.

### 3.7 ADMIN — public administration and public services (v2)

- **Participants.** Citizens and officials, patients and health staff.
- **Interaction.** Short encounters and appointments.
- **Register.** Administrative; health.
- **Language choice.** An institutional default plus the citizen's choice.
  Officials and health staff are subject to language requirements.
- **Policy levers.** The language of public services; requirements for public
  employees.
- **Calibration data.** EULP: language with doctors and administration *(to
  check)*.
- **v1:** no. Planned for v2 as a policy domain. Older adults' health contacts
  can be approximated by SERV in v1.

### 3.8 SOCIAL — friends and leisure

- **Participants.** Friends; members of associations and sports clubs.
- **Interaction.**
  - Meetings with friends, in pairs and groups.
  - Club activities.
  - Exposure is concentrated on a few strong ties.
- **Register.** Conversational, by age.
- **Language choice.** Relationship memory dominates. Friendship formation
  shows homophily (McPherson, Smith-Lovin & Cook, 2001), including linguistic
  homophily.
- **Network formation.** Friendships form through repeated contact in shared
  settings: class, work, club (Feld, 1981). Network size has a heavy tail, and
  tie strength varies.
- **Policy levers.** Support for associations and leisure in the minority
  language.
- **From legacy.** Friendship from shared context and repeated meetings,
  capacity, homophily, tie strength (legacy ideas §5.1).
- **Calibration data.** EULP: language with friends. Network-size
  distributions from social surveys *(to check)*.
- **v1:** yes.

### 3.9 PUBLIC — neighbourhood and public space

- **Participants.** Neighbours, strangers in the street and on transport.
- **Interaction.** Greetings and short exchanges with neighbours; overheard
  conversations.
- **Register.** Conversational.
- **Language choice.** MAXIMIN with perceived profiles; relationship memory
  with neighbours.
- **From legacy.** Bystanders overhearing conversations in the same place
  (legacy ideas §6.1).
- **Calibration data.** EULP: language with neighbours *(to check)*.
- **v1:** simple. This domain mainly adds overheard input and the cues for
  perceived profiles.

### 3.10 MEDIA — media and digital

- **Participants.** One agent and an exogenous source: TV, radio, streaming,
  press, social media, games.
- **Interaction.** One-way listening (reading in v2). There is no learning from
  speaking.
- **Register.** Media, by genre (subtitles corpora).
- **Language choice.** The **offer** (share of content per language, by genre
  and platform) times the **individual's preference**, which depends on
  proficiency (and attitudes in v2).
- **Policy levers.** Quotas; the public broadcaster's offer; dubbing and
  subtitling policy.
- **From legacy.** Sketched only (a stub, and a 2017 branch with a 20 %
  probability of media consumption).
- **Calibration data.** Audiences by language *(sources to check)*; time-use
  surveys.
- **v1:** exogenous input with a calibrated offer. Digital interaction between
  agents (messaging) waits for literacy (v2).

**Religion**, a classic domain in Fishman's work, is not modelled separately
in v1.

---

## 4. Mechanisms shared by all domains

### 4.1 Resolving the language of an event

The language of an event is resolved in this order. Each step can be switched
off for testing.

1. **Institutional norm** (class instruction, administration, workplace
   rule), if the setting has one.
2. **Relationship memory:** the language the participants have always used
   (dyads and groups), with renegotiation when proficiency changes.
3. **A motive-weighted choice** for new or mixed groups, among the languages
   the group can follow. It weighs:
   - **accommodation**: MAXIMIN, the language best known by the least
     competent participant (Van Parijs, 2011);
   - **perceived status**, in public domains;
   - **defence**: attachment × perceived threat, which can mean refusing to
     accommodate.

   See motives spec §6.
4. **Receptive multilingual mode:** when everyone understands both languages,
   each speaks their preferred one (ten Thije & Zeevaert, 2007).
5. **Initiator effect:** the opening move decides ties.
6. **Exclusion:** a participant who can neither speak nor understand is muted,
   and the experience is recorded (§4.4).

### 4.2 Sensing: perceived profiles

Real people do not know others' proficiency. They infer it from cues: accent,
first words, appearance, context. The legacy model used the true language
label. The new model should use a **perceived profile**: the true profile plus
noise, updated by experience with that person. This is what makes the
accommodation norm and the initiator effect realistic.

### 4.3 Exposure accounting

Every event produces, for each participant:
- words heard and spoken;
- per language and per register;
- directed or overheard;
- with a timestamp.

The events feed the learning core. They are also aggregated as outputs: words
per day by domain and language, comparable with daylong recordings and
experience sampling.

### 4.4 Exclusion and motivation

Muting, failed hiring and failed service encounters are recorded per agent and
language. A short-memory average of these experiences, measured in days,
drives motivated learning:
- self-study;
- joining conversations in the language;
- media in the language;
- in v2, adult classes and changes of network.

This comes from legacy ideas §9.

### 4.5 Time budget

Each life stage has a weekly schedule: weekdays vs weekends, school or work
days, holidays. It sets how often each domain's settings occur. Calibrate it
on time-use surveys. Each occurrence is a timestamped event, so memory sees
realistic spacing.

---

## 5. Population-level targets by domain

In the generic world, the domain targets are **stylised facts**. A receding
language retreats from public, high-status domains first and survives longest
at home (V34). Speakers of the lower-status language accommodate more (V35).

The indicators below are for the **specific-society phase**. They are
validation targets in
[`04_requirements_and_validation.md`](04_requirements_and_validation.md).

| Domain | Indicator | Source |
|---|---|---|
| HOME | language with parents vs with own children (transmission), by couple type | EULP |
| HOME | share of linguistically mixed couples | census or EULP *(to check)* |
| SCHOOL | knowledge by age cohort, showing the shift after schooling policy changed | census series since 1986 |
| WORK | language at work by sector | EULP *(to check sector detail)* |
| SERV, PUBLIC | language in shops and with strangers | EULP *(to check)* |
| SOCIAL | language with friends; linguistic homophily | EULP |
| MEDIA | consumption by language | audience surveys *(to check)* |
| All | habitual language and identification language | EULP |

---

## 6. Open questions for this document

1. **Domain list.** Is anything missing or unnecessary for v1? Candidates:
   religion; separate health; digital interaction between agents.
2. **Granularity of WORK.** How many sectors? Proposal: about 5–8 groups
   matching the labour-force survey and EULP categories.
3. **Space.** Municipalities as nodes, with settings inside them, and no grid
   (PROP-05 in [`06_decisions.md`](06_decisions.md)). Large cities
   (Barcelona) may need districts.
4. **Perceived profiles.** Adopt them in v1 (§4.2)? Recommended, because the
   accommodation norm depends on them.
5. **Order of the language-choice steps (§4.1).** Calibrate it per domain, or
   fix it?

## References

- Bialystok, E., Luk, G., Peets, K. F., & Yang, S. (2010). Receptive vocabulary differences in monolingual and bilingual children. *Bilingualism: Language and Cognition*, 13(4), 525–531.
- Feld, S. L. (1981). The focused organization of social ties. *American Journal of Sociology*, 86(5).
- Fishman, J. A. (1972). Domains and the relationship between micro- and macrosociolinguistics. In J. J. Gumperz & D. Hymes (eds.), *Directions in Sociolinguistics*. Holt, Rinehart & Winston.
- Fishman, J. A. (1991). *Reversing Language Shift*. Multilingual Matters.
- Giles, H., Coupland, N., & Coupland, J. (1991). Accommodation theory: communication, context, and consequence. In *Contexts of Accommodation*. Cambridge University Press.
- McPherson, M., Smith-Lovin, L., & Cook, J. M. (2001). Birds of a feather: homophily in social networks. *Annual Review of Sociology*, 27.
- Mehl, M. R., et al. (2007). Are women really more talkative than men? *Science*, 317(5834), 82.
- ten Thije, J. D., & Zeevaert, L. (eds.) (2007). *Receptive Multilingualism*. John Benjamins.
- Van Parijs, P. (2011). *Linguistic Justice for Europe and for the World*. Oxford University Press.
- Weisleder, A., & Fernald, A. (2013). Talking to children matters. *Psychological Science*, 24(11).
- Woolard, K. A. (1989). *Double Talk: Bilingualism and the Politics of Ethnicity in Catalonia*. Stanford University Press.
