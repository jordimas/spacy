# [CA] Model per a Spacy 3.0 de la llengua catalana

### Manual d'ús de l'Spacy: https://spacy.io/usage/spacy-101

#### To use our models, after installing:
```
import spacy

nlp = spacy.load("ca_core_web_md")

doc = nlp("Setze jutges d'un jutjat mengen fetge d'un penjat.")

for t in doc: print(t.text,"\t",t.lemma_)

```

Demo a: http://temu.bsc.es:8080

### Official catalan spacy models from Explosion coming soon with version 3.1.0
### BSC will continue generating its own, more experimental, models for quicker development cycles and testing new capabilities

# Versions

- **ca_base_web_trf** & **ca_core_web_trf** contenen un transformer basat en RoBERTA com a base per un entrenament multitasca dels diferents components. La versió "core" conté, a més, vectors FastText per mesurar la similud semàntica. La la versió "base" també pot mesurar la similitud semàntica, però ho fa a partir de NER, dependències i altres informacions.

- **ca_core_web_lg**, en canvi, fa servir els vectors FastText com a base per a l'entrenament dels components, de manera que no necesita transformers o GPU.

Aquesta és una publicació pre-producció. El release oficial serà ben aviat. 

Per ara, els syntax_iterators que s'usen per al chunking, els diccionaris de lematització i alguns altres components es troben incrustrats en el codi, enlloc de en els directoris habituals spacy/lang i spacy_lookups_data. Després del llançament oficial podrem posar cada component al directori que li correspon.

# [EN] Spacy 3.0 releases

Public release for catalan Spacy 3.0 models

Spacy usage basics: https://spacy.io/usage/spacy-101

Demo at: http://temu.bsc.es:8080

# Versions
### new versions 3.2.6
- **ca_base_web_trf** & **ca_core_web_trf** contain a Catalan RoBERTa-based transformer as a common backbone for multitask training of the different components. The latter one ("core") also contains FastText embeddings to measure lexical similarity, although the "base" version can also measure semantic similarity, but using NER, dependency and other information, not directly on a dedicated distance matrix.

- **ca_core_web_lg**, on the other hand, uses FastText embeddings as a training backbone, so it doesn't need transformers or GPUs.

These are the pre-production releases, and a spacy "official" release will be forthcoming. For now, the syntax_iterators (for chunking), the lemmatization dictionaries and other components,  as well as other tweaks, are embedded in code, outside of the usual spacy/lang directories or the spacy-lookup packages, and under the config/functions.py and the lemmas/ directory (that will be created when the project is run). 
We provide the training code for the "base" release, using spacy's project structure and facilities (https://spacy.io/usage/projects).  You can clone directly from this github repo.
The training data will be downloaded when you do the initialization of the project with:

``` python -m spacy project assets ```

# Installation:

## base model without word vectors:

```pip install https://github.com/TeMU-BSC/spacy/releases/download/3.2.6.2/ca_base_web_trf-3.2.6-py3-none-any.whl```

## core model with word embeddings for lexical similarity

```pip install hhttps://github.com/TeMU-BSC/spacy/releases/download/3.2.6.2/ca_core_web_trf-3.2.6-py3-none-any.whl```

## core model without BERTa transformer, but with Fasttext embeddings

```pip install https://github.com/TeMU-BSC/spacy/releases/download/3.2.6.2/ca_core_web_md-3.2.6-py3-none-any.whl```


## Non-wheel, tra.gzipped versions also available at https://github.com/TeMU-BSC/spacy/releases/tag/3.2.4gz

# Sources
Based on BERTa transformer, AnCora corpus annotations and UDEP treebanks, all merged into single training/dev corpora to enable simultaneous multi-task training.
https://github.com/TeMU-BSC/spacy/releases/download/3.2.6/ANCORA_ca.zip

## Transformer:

*bsc/roberta-base-ca-cased* @ Hugging Face, a RoBERTa transformer pretrained with the 1.760 million token Catalan Text Corpus (https://doi.org/10.5281/zenodo.4519348) 

## Dependency Treebank, XPOS, sentence segmentation

From version 3.6 of the Catalan Universal Dependencies (https://universaldependencies.org/ca/) project treebank, with changes for pronouns and multi-word tokenization 


## Lemmatization

Adaptation of French lemmatizer, using  word lists and corpus frequencies developed in house.

https://github.com/TeMU-BSC/spacy/releases/download/v3.2.4lemmas/lemmas.zip

## Named Entity Recognition

From original AnCora corpus (https://doi.org/10.5281/zenodo.4529299)

## Word vectors ("core" model only)

From FastText word embeddings: https://doi.org/10.5281/zenodo.4522040


# External evaluation on test split for ca_base_web_trf:
```
  "token_acc":0.9996689501,
  "tag_acc":0.9866830883,
  "pos_acc":0.9864785119,
  "morph_acc":0.9722713864,
  "lemma_acc":0.9679711664,
  "dep_uas":0.9409872785,
  "dep_las":0.9182501866,
  "ents_p":0.9153339605,
  "ents_r":0.9136150235,
  "ents_f":0.9144736842,
  "sents_p":0.9861538462,
  "sents_r":0.9922600619,
  "sents_f":0.9891975309,
  "speed":4129.6607627658
```
<!---## Text Classification (To come)

From TeCla corpus based on Agencia Catalana de Noticias Newswire
(https://doi.org/10.5281/zenodo.4627197)-->


<!---
# Includes:

* Noun Chunks

* NERC

* Coarse XPOS tags

* Dependency parsing

* lookup-based lemmatization with POS disambiguation

* BERTa-based transformer

* tokenization and sentence segmentation

* Morphological analysis

* Static word vectors (in core models)

## To come:
* Fine-grained Parole/Eagles POS tags

* Text classification  


