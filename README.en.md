# The Influence of Empathy in Large Language Models on Decision-Making in Game Theory

<p align="center">
  <b>Master's Thesis</b><br>
  National University of Science and Technology MISIS · Institute of Computer Sciences ·
  Department of Infocommunication Technologies<br>
  Moscow, 2024
</p>

<p align="center">
  <a href="https://github.com/ivanmakovetskiy/diplom/actions/workflows/build.yml"><img src="https://github.com/ivanmakovetskiy/diplom/actions/workflows/build.yml/badge.svg" alt="Build LaTeX documents"></a>
  <img src="https://img.shields.io/badge/LaTeX-XeLaTeX%20%2B%20Biber-blue" alt="XeLaTeX + Biber">
  <img src="https://img.shields.io/badge/type-Master%27s%20thesis-green" alt="Master's thesis">
  <img src="https://img.shields.io/badge/year-2024-lightgrey" alt="2024">
  <a href="LICENSE"><img src="https://img.shields.io/badge/template-CC%20BY%204.0-orange" alt="CC BY 4.0"></a>
</p>

[Русский](README.md) | **English**

| | |
|---|---|
| **Author** | Ivan A. Makovetskiy ([@ivanmakovetskiy](https://github.com/ivanmakovetskiy)), group MIVT-22-5 |
| **Supervisor** | Ilya A. Makarov, PhD |
| **University** | National University of Science and Technology MISIS, Moscow, Russia |
| **Programme** | 09.04.01 Informatics and Computer Engineering |
| **Document type** | Master's thesis (defended in 2024), written in Russian |

---

## Abstract

This thesis investigates how empathy and emotions embedded in large language models (LLMs) alter
strategies and outcomes of decision-making in game-theoretic scenarios and ethical dilemmas. It
explores methods for integrating empathy into language models and analyses how an agent's emotional
state affects its cooperative behaviour, propensity to defect, and the alignment of its decisions
with human behaviour.

An experimental framework based on emotional prompting is proposed: a model receives a game
description, an emotional state, and interaction context, and its decisions are then compared across
models, emotions, languages, and partner strategies.

**Keywords:** empathy, large language models, decision making, game theory, cooperative behaviour,
game scenarios, empathy integration, agent behaviour, alignment.

<p align="center">
  <img src="images/framework_overview.png" alt="LLM decision-making pipeline in a game context" width="620"><br>
  <em>Framework overview: LLM decision-making in a game context (Chapter 2)</em>
</p>

## Experimental setup

| Component | Details |
|---|---|
| **Games** | Dictator Game, Prisoner's Dilemma, Public Goods Game (one-shot and repeated) |
| **Ethics benchmarks** | TrustLLM: explicit ethics (MoralChoice), implicit ethics (ETHICS), stereotype recognition (StereoSet) |
| **Emotions** | Five basic Ekman emotions: anger, sadness, happiness, disgust, fear |
| **Prompting strategies** | Simple (emotion without context), co-player (emotion caused by the partner), external (emotion from outside the game) |
| **Models** | GPT-3.5, GPT-4, GPT-4o, Claude 3 Haiku, Claude 3 Opus, LLaMA-2 (13B/70B), Mixtral-8x7B, OpenChat-7B, GigaChat, Command R+ |
| **Languages** | English, German, Russian, Chinese, Arabic |
| **APIs** | OpenAI, Anthropic, Hugging Face, OpenRouter |

## Key findings

- Emotional prompting can substantially shift LLM decisions; **anger prompting breaks alignment
  even in GPT-4**, producing a human-like emotional reaction with no empathy towards the partner.
- Current LLMs are not yet ready for autonomous decision-making in strategic environments due to
  emotional and strategic biases; the effect is strongest in **open-weight and smaller models**.
- Emotions affect model ethics unevenly: anger and disgust most often degrade stereotype
  recognition and ethical judgments (LLaMA, OpenChat, Claude Opus), whereas GPT-4o is notably
  resilient, and "happiness" can even improve its accuracy.
- Empathy and awareness of a partner's emotional state can increase agents' cooperativeness and
  improve joint outcomes, so the emotional factor should be taken into account in LLM alignment.

The results of this work were used in papers submitted to the ACM Conference on Economics &
Computation 2024 and NeurIPS 2024; a draft of the paper *"EAI: Emotional Decision-Making of LLMs
in Strategic Games and Ethical Dilemmas"* is kept in [`Styles/`](Styles/) (`Styles/paper.tex`).

## Thesis outline

- **Chapter 1. Theoretical background** — the concept of empathy; empathy in large language
  models; LLMs in game-theoretic settings.
- **Chapter 2. Methodology** — problem statement; game scenarios; the framework and the models
  used; game prompts; the experimental pipeline.
- **Chapter 3. Results** — the effect of emotions on LLM biases and ethics; results for the
  Dictator Game, Prisoner's Dilemma, and Public Goods Game; the multilingual setting; consistency
  of the results.

## Repository structure

```text
.
├── dissertation.tex        # Main thesis file
├── synopsis.tex            # Thesis synopsis (template scaffold)
├── presentation.tex        # Defence presentation (template scaffold)
├── Dissertation/           # Chapters and aux files of the thesis
│   ├── part1.tex … part3.tex
│   ├── introduction.tex / conclusion.tex / annotation.tex
│   ├── appendix.tex, dictionary.tex, acronyms.tex
│   └── images/             # Incl. the signed title page (signed.pdf)
├── Synopsis/               # Synopsis sources
├── Presentation/           # Presentation sources
├── common/                 # Shared settings; data.tex — thesis metadata
├── biblio/                 # Bibliography (external.bib — ~200 references, author.bib)
├── images/                 # Shared figures (Chapters 2–3)
├── Styles/                 # EAI paper materials (paper.tex, NeurIPS style, plots in img/)
├── Readme/                 # Installation, bibliography, links; original template README
├── Makefile, latexmkrc     # Build system (XeLaTeX + Biber)
└── .github/workflows/      # CI: automatic PDF builds
```

> **Built PDFs are not stored in the repository.** They are produced automatically:
> see the artifacts of the latest run in the **Actions** tab or the files in **Releases**.
> The only PDFs kept in git are build inputs that cannot be regenerated (the signed
> title page and a few vector figures).

## Building the PDFs

You need TeX Live (XeLaTeX + Biber) and `make`. See
[Readme/Installation.md](Readme/Installation.md) for software installation details.

```bash
git clone https://github.com/ivanmakovetskiy/diplom.git
cd diplom

make dissertation     # → dissertation.pdf
make synopsis         # → synopsis.pdf
make presentation     # → presentation.pdf
make                  # all three documents

make clean            # remove build artifacts
make distclean        # remove build artifacts and built PDFs
```

Fonts are configured in [`usercfg.mk`](usercfg.mk): the default is `FONTFAMILY=1`
(MS fonts, targeting Windows). On Linux it is easier to build with the free,
metrically compatible Liberation fonts:

```bash
make dissertation FONTFAMILY=2   # Liberation
```

Alternatives: build in Docker (`Dockerfile`, `install-dockertex.sh`) or in Overleaf
(upload the repository as a project and select the XeLaTeX compiler).

On every push to `main`, GitHub Actions rebuilds all PDFs and attaches them as run
artifacts; pushing a `v*` tag additionally publishes them to Releases.

## How to cite

```bibtex
@mastersthesis{makovetskiy2024empathy,
  author  = {Makovetskiy, Ivan A.},
  title   = {The Influence of Empathy in Large Language Models
             on Decision-Making in Game Theory},
  school  = {National University of Science and Technology MISIS},
  address = {Moscow, Russia},
  year    = {2024},
  note    = {Master's thesis, programme 09.04.01; supervisor --- Ilya A. Makarov, PhD.
             Original title (in Russian): Issledovanie vliyaniya e`mpatii v bol'shikh
             yazy`kovy`kh modelyakh v protsesse prinyatiya reshenij v teorii igr},
  url     = {https://github.com/ivanmakovetskiy/diplom}
}
```

A machine-readable description is provided in [`CITATION.cff`](CITATION.cff).

## Template and licence

The thesis is typeset according to Russian standard GOST R 7.0.11-2011 using the
[Russian-Phd-LaTeX-Dissertation-Template](https://github.com/AndreyAkinshin/Russian-Phd-LaTeX-Dissertation-Template)
(by Andrey Akinshin et al.; the original template README with the full list of its authors is
preserved in [Readme/Template-README.md](Readme/Template-README.md)).

- The typesetting template is distributed under **CC BY 4.0** (see [LICENSE](LICENSE)): it may be
  modified and used in any way provided the template authorship is preserved.
- All rights to the **text and results of this thesis** belong to its author.
