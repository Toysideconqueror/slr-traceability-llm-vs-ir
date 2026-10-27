# Systematic Literature Review: LLMs vs. Information Retrieval for Requirements-to-Code Traceability

Systematic literature review (SLR) on **requirements-to-source-code traceability link recovery (TLR)**:
do large language models (GPT-4 class, zero-/few-shot) outperform classic information-retrieval baselines (VSM, LSI, BM25)?

Course project for **SWR302 – Software Requirements**, FPT University HCMC (2026). Team 2 project; this repository holds the
part done by **Nguyễn Dương Thiên Ý** (team leader): the IEEE Xplore search, the two screening rounds and the gap analysis G1.

## Protocol

Inclusion / exclusion criteria: [`protocol/inclusion-exclusion-criteria.md`](protocol/inclusion-exclusion-criteria.md)
(peer-reviewed English papers from 2020 on, with empirical results, targeting requirement-to-code traceability at class level with LLM or IR techniques;
code summarisation, bug localisation and fault prediction are out of scope).

Search (IEEE Xplore, 05/07/2026) – exact strings and per-query counts in [`protocol/search-log.md`](protocol/search-log.md):

| Query | Focus | Results |
|---|---|---:|
| Q1 | LLM + traceability link recovery | 14 |
| Q2 | prompting techniques for requirements / source code | 550 |
| Q3 | IR baselines (VSM, LSI, BM25) for traceability | 362 |
| Q4 | hallucination in LLMs for code / links | 671 |

Q2 and Q4 were deliberately broad and mostly removed at the first screening round.

## Screening flow (PRISMA)

```
IEEE Xplore records from 4 queries ............ 1,597
After removing cross-query duplicates ......... 1,577
  Round 1 (metadata): excluded ................ 1,442   (IC-P 1,147 · IC-Y 254 · EC-O 41)
Round 2 (abstract) ............................   135   (101 include · 34 unsure, carried over)
  Round 2: excluded ...........................   105
Passed abstract screening ......................    30
Full text obtained for ........................    10 distinct papers
```

Every record, with its decision and reason code at each round, is in
[`screening/screening_records.csv`](screening/screening_records.csv) (`v1_*` = round 1, `v2_*` = round 2).
Abstracts are not included (publisher copyright) – use the DOI to retrieve them.

### Papers with full text reviewed

| Paper | Year | Venue | DOI |
|---|---:|---|---|
| Improving the Effectiveness of Traceability Link Recovery using Hierarchical Bayesian Networks | 2020 | 2020 IEEE/ACM 42nd International Conference on Software Engineering (ICSE) | — |
| Traceability Transformed: Generating More Accurate Links with Pre-Trained BERT Models | 2021 | 2021 IEEE/ACM 43rd International Conference on Software Engineering (ICSE) | [10.1109/ICSE43902.2021.00040](https://doi.org/10.1109/ICSE43902.2021.00040) |
| An Empirical Study on Source Code Feature Extraction in Preprocessing of IR-Based Requirements Traceability | 2022 | 2022 IEEE 22nd International Conference on Software Quality, Reliability and Security (QRS) | [10.1109/QRS57517.2022.00110](https://doi.org/10.1109/QRS57517.2022.00110) |
| Enhancing Traceability Link Recovery with Unlabeled Data | 2022 | 2022 IEEE 33rd International Symposium on Software Reliability Engineering (ISSRE) | [10.1109/ISSRE55969.2022.00050](https://doi.org/10.1109/ISSRE55969.2022.00050) |
| Generating and Visualizing Trace Link Explanations | 2022 | 2022 IEEE/ACM 44th International Conference on Software Engineering (ICSE) | [10.1145/3510003.3510129](https://doi.org/10.1145/3510003.3510129) |
| MLTracer: An Approach Based on Multi-Layered Gradient Boosting Decision Trees for Requirements Traceability Recovery | 2024 | 2024 International Joint Conference on Neural Networks (IJCNN) | [10.1109/IJCNN60899.2024.10651499](https://doi.org/10.1109/IJCNN60899.2024.10651499) |
| Requirements Classification for Traceability Link Recovery | 2024 | 2024 IEEE 32nd International Requirements Engineering Conference (RE) | [10.1109/RE59067.2024.00024](https://doi.org/10.1109/RE59067.2024.00024) |
| TRIAD: Automated Traceability Recovery based on Biterm-enhanced Deduction of Transitive Links among Artifacts | 2024 | 2024 IEEE/ACM 46th International Conference on Software Engineering (ICSE) | [10.1145/3597503.3639164](https://doi.org/10.1145/3597503.3639164) |
| LiSSA: Toward Generic Traceability Link Recovery Through Retrieval-Augmented Generation | 2025 | 2025 IEEE/ACM 47th International Conference on Software Engineering (ICSE) | [10.1109/ICSE55347.2025.00186](https://doi.org/10.1109/ICSE55347.2025.00186) |
| AI-Assisted Requirements Traceability for Industrial Software: An Empirical Study | 2026 | 2026 IEEE International Conference on Software Analysis, Evolution and Reengineering (SANER) | [10.1109/SANER67736.2026.00100](https://doi.org/10.1109/SANER67736.2026.00100) |

## Gap analysis (G1)

[`analysis/gap-analysis.md`](analysis/gap-analysis.md) (Vietnamese): no paper in the reviewed set fine-tunes a modern LLM for TLR –
modern LLMs are only used through prompting or RAG, while fine-tuning appears only with older BERT-style models.
The document includes a counter-evidence check, a feasibility check (datasets SEOSS / CoEST, QLoRA on Llama 3.1 8B,
baselines GPT-4o + CoT and T-BERT) and the formal gap statement. This gap became the basis of the team's follow-up research proposal.

## Repository layout

```
├── protocol/    inclusion/exclusion criteria, search log
├── screening/   all 1,577 records with round-1 and round-2 decisions (CSV)
└── analysis/    gap analysis G1
```

## Limitations

- This repository covers one database (IEEE Xplore); the other team members searched and analysed separately and their material is not included.
- Full text was obtained for 10 of the 30 papers that passed abstract screening, so evidence extraction is partial.
- Papers (PDFs) and abstracts are not redistributed.
