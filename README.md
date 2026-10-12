# CitiLink-News

**CitiLink-News** is a dataset for studying the newsworthiness of discussion subjects in Portuguese municipal council meeting minutes and the generation of texts in news format from those subjects.

It is derived from discussion-subject segments previously identified in **CitiLink-Minutes**. The unit of analysis is therefore a **segment corresponding to a discussion subject**, rather than a complete municipal meeting minute.

> **Repository scope**
>
> This GitHub repository contains **documentation and a small sample only**.  
> The complete CitiLink-News dataset is **not distributed through GitHub**. Its full release will be handled through the **INESC TEC Research Data Repository (RDM)** after the corresponding scientific, legal and data-governance review.

## Dataset overview

CitiLink-News contains two complementary components that were created for different experimental purposes.

### 1. Newsworthiness component

This component supports the computational modelling of newsworthiness.

It contains **1,207 segments from 53 municipal meeting minutes with final binary newsworthiness labels**. Each labelled segment is associated with:

- a binary newsworthiness decision (`binary_label`):
  - `0` — non-newsworthy
  - `1` — newsworthy
- seven news values, each annotated on an ordinal scale from **1 to 5**:
  - `relevancia`
  - `proximidade`
  - `novidade`
  - `atualidade`
  - `continuidade`
  - `notoriedade`
  - `negatividade`
- a weighted **Public Interest Index (IIP)** in the interval `[0, 1]`.

The binary decision is a **separate human annotation**. It is not obtained by thresholding the news values or the IIP.

The IIP aggregates the seven news values using the following weights:

| News value | Weight |
|---|---:|
| Relevância | 30% |
| Proximidade | 20% |
| Novidade | 15% |
| Atualidade | 10% |
| Continuidade | 10% |
| Notoriedade | 10% |
| Negatividade | 5% |

Each 1–5 score is first mapped to `[0, 1]` and then combined using the weights above.

### 2. Generation component

This component supports experiments on the generation of texts in news format.

It contains **2,769 segment–reference pairs from 116 municipal meeting minutes**. Each segment is associated with a **synthetic reference news text produced with Gemini 2.5 Pro**.

The reference structure contains:

- `antetitulo`
- `titulo`
- `superlead`
- `lead`
- `corpo`

`titulo`, `lead` and `corpo` are the required fields. `antetitulo` and `superlead` may be empty.

The synthetic references are intended to provide a common experimental target for comparing generation models. They must **not** be interpreted as individually journalist-validated gold-standard news articles.

## Why the two components have different sizes

The two components were produced for different tasks and do not cover the same subset of CitiLink-Minutes.

The **newsworthiness component** is based on the subset of segments that received human newsworthiness annotations. The **generation component** was created over a broader set of available segments from 116 meeting minutes.

Consequently, the number of synthetic reference news texts is larger than the number of segments with final human binary newsworthiness labels.

## Relationship with CitiLink-Minutes

CitiLink-News builds on the segmentation and municipal-meeting structure provided by **CitiLink-Minutes**.

CitiLink-Minutes:

- contains the municipal meeting minutes and their multilayer annotations;
- defines the boundaries of the discussion subjects used here as segments;
- provides the source document structure from which CitiLink-News was derived.

Official CitiLink-Minutes repository:

https://github.com/INESCTEC/citilink-dataset

CitiLink-Minutes dataset DOI:

https://doi.org/10.25747/7KG6-1K22

## Sample data

The repository contains three illustrative records for each component:

```text
sample_data/
├── newsworthiness_sample.jsonl
└── generation_sample.jsonl
```

The same segment identifiers are used in the two sample files when a segment is represented in both components. This makes it possible to inspect how the same source segment is represented for the two tasks.

These files are **illustrative samples only** and are not intended to reproduce the complete dataset.

### Newsworthiness sample schema

Example structure:

```json
{
  "segment_id": "string",
  "minute_id": "string",
  "municipality": "string",
  "begin": 0,
  "end": 0,
  "text": "string",
  "theme": "string",
  "news_values": {
    "relevancia": 1,
    "proximidade": 1,
    "novidade": 1,
    "atualidade": 1,
    "continuidade": 1,
    "notoriedade": 1,
    "negatividade": 1
  },
  "iip": 0.0,
  "binary_label": 0
}
```

### Generation sample schema

Example structure:

```json
{
  "segment_id": "string",
  "minute_id": "string",
  "municipality": "string",
  "date": "YYYY-MM-DD",
  "begin": 0,
  "end": 0,
  "text": "string",
  "theme": "string",
  "reference_news": {
    "antetitulo": "string",
    "titulo": "string",
    "superlead": "string",
    "lead": "string",
    "corpo": "string"
  }
}
```


## Public sample

The files under `sample_data/` are **illustrative public samples**. The selected records were reviewed before inclusion in this repository, and personal names or obvious personal identifiers present in the sample text were replaced with neutral placeholders such as `[PESSOA]` and `[IDENTIFICADOR]`.

Municipality names and public or institutional entities were preserved because they are part of the documentary and experimental context. The complete dataset is not distributed through GitHub and will be subject to the corresponding institutional, legal and data-governance review before publication in the INESC TEC Research Data Repository (RDM).

## Annotation guidelines

The newsworthiness annotation guidelines used in CitiLink-News are available here:

- [CitiLink-News Annotation Guidelines — Version 1.0](docs/citilink_news_annotation_guidelines_v1.0.pdf)

They define the unit of analysis, the seven news values and their 1–5 scales, and the independent binary newsworthiness decision.

The annotation guidelines for the source CitiLink-Minutes resource are available in its official repository:

- https://github.com/INESCTEC/citilink-dataset/blob/master/docs/citilink_annotation_guidelines.pdf

## Full dataset access

The complete CitiLink-News dataset is **not hosted in this repository**.

The complete resource is intended to be deposited in the **INESC TEC Research Data Repository (RDM)** after validation by the project team and the applicable legal/data-governance process.

The definitive RDM DOI, access conditions and citation information should be added to this README when that process is complete.

## Access and licensing

CitiLink-News is derived from CitiLink-Minutes and includes annotations and synthetic references created for the newsworthiness and generation tasks.

The **final access and licensing conditions for the complete CitiLink-News dataset will be defined in the INESC TEC RDM record** following institutional review.

The underlying CitiLink-Minutes resource is distributed under the **Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND 4.0)** licence and is subject to the access conditions described in its official repository and RDM record.

This repository should therefore not be interpreted as granting access to, or defining the final licence of, the complete CitiLink-News dataset.

## Citation

The definitive citation for CitiLink-News will be added after publication of the complete dataset in the INESC TEC RDM.

Because CitiLink-News is derived from CitiLink-Minutes, users should also cite the source dataset:

```bibtex
@dataset{citilink2025,
  author      = {Ricardo Campos and Ana Filipa Pacheco and Ana Luísa Fernandes and
                 Inês Cantante and Rute Rebouças and Luís Filipe Cunha and José Isidro and
                 José Evans and Miguel Marques and Rodrigo Batista and Evelin Amorim and
                 Alípio Jorge and Nuno Guimarães and Sérgio Nunes and António Leal and
                 Purificação Silvano},
  title       = {CitiLink-Minutes: A Multilayer Annotated Dataset of Municipal Meeting Minutes},
  year        = {2025},
  doi         = {10.25747/7KG6-1K22},
  url         = {https://doi.org/10.25747/7KG6-1K22},
  institution = {INESC TEC}
}
```

Associated paper:

```bibtex
@inproceedings{citilinkminutes2026,
  author    = {Ricardo Campos and Ana Filipa Pacheco and Ana Luísa Fernandes and
               Inês Cantante and Rute Rebouças and Luís Filipe Cunha and José Isidro and
               José Evans and Miguel Marques and Rodrigo Batista and Evelin Amorim and
               Alípio Jorge and Nuno Guimarães and Sérgio Nunes and António Leal and
               Purificação Silvano},
  title     = {CitiLink-Minutes: A Multilayer Annotated Dataset of Municipal Meeting Minutes},
  booktitle = {Advances in Information Retrieval},
  year      = {2026},
  pages     = {511--527},
  publisher = {Springer Nature Switzerland},
  doi       = {10.1007/978-3-032-21321-1_56},
  url       = {https://doi.org/10.1007/978-3-032-21321-1_56}
}
```

## Project and acknowledgements

CitiLink-News was developed in the context of the **CitiLink — Enhancing Municipal Transparency and Citizen Engagement through AI: From Unstructured to Structured Data** project and as part of the Master's dissertation of **Tassia da Silva de Carvalho**, under the scientific supervision of Ricardo Campos and co-supervision of Purificação Silvano.

The annotation work combines contributions from computer science, linguistics and communication/journalism research. The CitiLink-News annotation guidelines were prepared by Purificação Silvano, Sara Nerea, Raquel Sequeira, Inês Cantante, Rute Rebouças and Ricardo Campos.

CitiLink project:

https://citilink.inesctec.pt/

This work was developed with the participation of **INESC TEC**, including the **NLP & IR** research group, and the University of Beira Interior and University of Porto.


## Contact

For questions regarding CitiLink and the dataset publication process:

**citilink@inesctec.pt**
