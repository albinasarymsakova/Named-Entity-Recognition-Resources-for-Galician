# Named Entity Recognition Resources for Galician

This repository contains Named Entity Recognition annotated corpora for the Galician language. These resources are made available under the terms of the Creative Commons Attribution 4.0 International Public License (CC BY 4.0) (which you can find at https://creativecommons.org/licenses/by/4.0/), and are distributed without any warranty.

## Contents

The corpora are located in the [`dataset/`](dataset/) directory, split into training, development, and test material:

```
dataset/
├── train/
│   └── train_sli_nerc_treegal_esp_ancora_freeling_pt.json
├── dev/
│   └── SLI_NERC_dev.json
└── test/
    ├── CorNER_test.json
    ├── Galician_PUD_test.json
    ├── LREC_test.json
    ├── SLI_NERC_test.json
    ├── Treegal_test.json
    └── mixed_test.json
```

- **train** – a combined training corpus built from the following resources:
  - **SLI NERC** – the train split of the SLI NERC corpus (Agerri et al., 2018). We rely on the splits of this corpus released by Garcia (2024): https://github.com/marcospln/evaluation_splits_gl
  - **TreeGal** – the train split of the UD Galician-TreeGal corpus (Garcia et al., 2018), released within this repository as a newly annotated Galician NER resource.
  - **Spanish AnCora** dataset (Taulé et al., 2008), converted to IOB format from its UD version: https://github.com/UniversalDependencies/UD_Spanish-AnCora
  - **Portuguese Bosque** dataset (https://www.linguateca.pt/floresta/corpus.html#bosque) as released by Pires (2017).
- **dev** – the development split of the SLI NERC corpus (Agerri et al., 2018).
- **test** – five test sets, each from a different source, plus their concatenation:
  - **CorNER** (`CorNER_test.json`) – based on the CorNER corpus (Garcia et al., 2012).
  - **Galician PUD** (`Galician_PUD_test.json`) – a newly annotated Galician NER resource, based on the Galician PUD dataset released by Sánchez-Rodríguez et al. (2024).
  - **LREC** (`LREC_test.json`) – based on the corpus released by Garcia and Gamallo (2014).
  - **SLI NERC** (`SLI_NERC_test.json`) – the test split of the SLI NERC corpus (Agerri et al., 2018).
  - **TreeGal** (`Treegal_test.json`) – the test split of the UD Galician-TreeGal treebank (Garcia et al., 2018).
  - **mixed** (`mixed_test.json`) – the concatenation of the five test sets above.

## Data format

Each file is in **JSON Lines** format: one JSON object per line, one object per sentence. Every object has two parallel lists of equal length:

- `tokens` – the list of tokens in the sentence.
- `labels` – the corresponding NER tag for each token.

Example line:

```json
{"tokens": ["Jorquera", "carga", "contra", "a", "propaganda", "de", "o", "Códice"],
 "labels": ["B-PER", "O", "O", "O", "O", "O", "O", "B-MISC"]}
```

### Tag set

Entities are annotated with the **BIO (IOB2)** scheme over four entity types, following the CoNLL-2002/2003 convention:

| Entity type | Description |
|-------------|-------------|
| `PER`  | person |
| `LOC`  | location |
| `ORG`  | organisation |
| `MISC` | miscellaneous |

## Statistics

| Split | File | Sentences | Tokens | Entities |
|-------|------|----------:|-------:|---------:|
| train | `train_sli_nerc_treegal_esp_ancora_freeling_pt.json` | 33,624 | 983,139 | 52,765 |
| dev   | `SLI_NERC_dev.json` | 415 | 16,254 | 1,084 |
| test  | `CorNER_test.json` | 696 | 20,932 | 924 |
| test  | `Galician_PUD_test.json` | 1,000 | 23,509 | 1,246 |
| test  | `LREC_test.json` | 1,707 | 47,254 | 3,318 |
| test  | `SLI_NERC_test.json` | 1,654 | 40,405 | 1,568 |
| test  | `Treegal_test.json` | 400 | 10,112 | 488 |
| test  | `mixed_test.json` | 5,457 | 142,212 | 7,544 |

Entity counts per type:

| File | PER | LOC | ORG | MISC |
|------|----:|----:|----:|-----:|
| `train_sli_nerc_treegal_esp_ancora_freeling_pt.json` | 13,610 | 10,287 | 17,338 | 11,530 |
| `SLI_NERC_dev.json` | 354 | 200 | 422 | 108 |
| `CorNER_test.json` | 121 | 280 | 438 | 85 |
| `Galician_PUD_test.json` | 420 | 399 | 276 | 151 |
| `LREC_test.json` | 1,184 | 543 | 805 | 786 |
| `SLI_NERC_test.json` | 213 | 439 | 556 | 360 |
| `Treegal_test.json` | 141 | 110 | 150 | 87 |
| `mixed_test.json` | 2,079 | 1,771 | 2,225 | 1,469 |

## Usage

Reading the data in Python:

```python
import json

def read_conll_json(path):
    with open(path, encoding="utf-8") as f:
        for line in f:
            line = line.strip()
            if line:
                obj = json.loads(line)
                yield obj["tokens"], obj["labels"]

for tokens, labels in read_conll_json("dataset/test/mixed_test.json"):
    ...
```

## How to cite

If you use these resources, please cite the paper that describes them:

```bibtex

@article{,

}
```

## References

Full citations for the source corpora:

```bibtex
@article{garcia2024training,
  title={Training and evaluation of vector models for Galician},
  author={Garcia, Marcos},
  journal={Language Resources and Evaluation},
  pages={1--44},
  year={2024},
  url = "https://doi.org/10.1007/s10579-024-09740-0",
  publisher={Springer}
}

@inproceedings{agerri-etal-2018-developing,
    title = "Developing New Linguistic Resources and Tools for the {G}alician Language",
    author = "Agerri, Rodrigo  and
      G{\'o}mez Guinovart, Xavier  and
      Rigau, German  and
      Solla Portela, Miguel Anxo",
    booktitle = "Proceedings of the Eleventh International Conference on Language Resources and Evaluation ({LREC} 2018)",
    month = may,
    year = "2018",
    address = "Miyazaki, Japan",
    publisher = "European Language Resources Association (ELRA)",
    url = "https://aclanthology.org/L18-1367",
}

@article{garcia2018new,
  title={{New treebank or repurposed? On the feasibility of cross-lingual parsing of romance languages with universal dependencies}},
  author={Garcia, Marcos and G{\'o}mez-Rodr{\'\i}guez, Carlos and Alonso, Miguel A},
  journal={Natural Language Engineering},
  volume={24},
  number={1},
  pages={91--122},
  year={2018},
  publisher={Cambridge University Press}
}

@inproceedings{taule-etal-2008-ancora,
    title = "{A}n{C}ora: Multilevel Annotated Corpora for {C}atalan and {S}panish",
    author = "Taul{\'e}, Mariona  and
      Mart{\'\i}, M. Ant{\`o}nia  and
      Recasens, Marta",
    booktitle = "Proceedings of the Sixth International Conference on Language Resources and Evaluation ({LREC}'08)",
    month = may,
    year = "2008",
    address = "Marrakech, Morocco",
    publisher = "European Language Resources Association (ELRA)",
    url = "http://www.lrec-conf.org/proceedings/lrec2008/pdf/35_paper.pdf",
    pages={96--101}
}

@mastersthesis{pires2017named,
  title={{Named entity extraction from Portuguese web text}},
  author={Pires, Andr{\'e} Ricardo Oliveira},
  year={2017},
  school={Universidade do Porto}
}

@inproceedings{garcia-gamallo-2014-multilingual,
    title = "Multilingual corpora with coreferential annotation of person entities",
    author = "Garcia, Marcos  and
      Gamallo, Pablo",
    booktitle = "Proceedings of the Ninth International Conference on Language Resources and Evaluation ({LREC}'14)",
    month = may,
    year = "2014",
    address = "Reykjavik, Iceland",
    publisher = "European Language Resources Association (ELRA)",
    url = "http://www.lrec-conf.org/proceedings/lrec2014/pdf/918_Paper.pdf",
    pages = "3229--3233"
}

@article{Garcia-Gayo-González-López-2012,
  title={Identifica{\c{c}}{\~a}o e classifica{\c{c}}{\~a}o de entidades mencionadas em galego},
  author={Garcia, Marcos and Gayo, Iria and Gonz{\'a}lez L{\'o}pez, Isaac},
  journal={Estudos de Ling{\"u}{\'\i}stica Galega},
  volume={4},
  year={2012},
  url={https://revistas.usc.gal/index.php/elg/article/view/401}
}

@inproceedings{sanchez-rodriguez-etal-2024-increasing,
    title = "Increasing manually annotated resources for {G}alician: the Parallel {U}niversal {D}ependencies Treebank",
    author = "S{\'a}nchez-Rodr{\'\i}guez, Xulia  and
      Sarymsakova, Albina  and
      Castro, Laura  and
      Garcia, Marcos",
    booktitle = "Proceedings of the 16th International Conference on Computational Processing of Portuguese",
    month = mar,
    year = "2024",
    address = "Santiago de Compostela, Galicia/Spain",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2024.propor-1.65",
    pages = "587--592"
}
```

## Information and contact

- Albina Sarymsakova — albina.sarymsakova.es@gmail.com
- Marcos Garcia — marcos.garcia.gonzalez@usc.gal
