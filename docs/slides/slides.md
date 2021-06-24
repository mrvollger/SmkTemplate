---
marp: true
theme: defualt
auto-scaling: true   
size: 4:3
paginate: true
footer: "
![Licence](https://img.shields.io/github/license/mrvollger/SmkTemplate?color=purple&label=MRV&style=for-the-badge)
[![Twitter URL](https://img.shields.io/twitter/follow/mrvollger?color=1DA1F2&label=twitter&style=for-the-badge)](https://twitter.com/mrvollger)
[![Github badge](https://img.shields.io/github/stars/mrvollger?label=github&style=for-the-badge&color=black)](https://github.com/mrvollger)
[![Website](https://img.shields.io/website?down_color=gray&style=for-the-badge&up_color=green&url=https%3A%2F%2Fmrvollger.github.io%2F)](https://mrvollger.github.io)
"
---

<!-- headingDivider: 2 -->
<style>
  footer {
      height: 10px;
  }
  footer img {
    height: 20px;
    float: center;
  }
  section {
     font-size: 22px; 
  }
  section.small {
    font-size: 18px; 
  }
  b, strong {
     color: #48c;
  }
</style>

# Creating publication quality workflows with **Snakemake** and **GitHub**

#### _Mitchell R. Vollger_

## **Who** is this for?

#### This guide is for people who already know the basics of **Snakemake** and **GitHub** and want to increase the usability of their work.

#### You should seriously consider using this guide if you plan to:

- **Reuse** a workflow in the future
- **Share** a workflow with anyone
- **Publish** a workflow

## **What** constitutes a publication quality workflow

- **Documented**
  - The workflow is described as well as all configuration options
- **Portable**
  - Your workflow can be downloaded, installed, and run successfully on a test set in less than ~10 minutes
- **Tested**
  - The workflow (and all changes to the workflow) are tested against a small data set continuously
- **Readable**
  - The code and directory layout are constructed in a readable and expected fashion

# **What** a publication quality workflow looks like

<!-- _class: section small-->

```bash
├── README.md # Must contain keywords snakemake and workflow
├── LICENSE.md # I use MIT
├── workflow
│   ├── rules # snakemake files (must have .smk suffix)
│   │   ├── module.smk
│   ├── envs # conda yaml(s)
│   │   ├── env.yaml
│   │   └── R.yaml
│   ├── scripts # scripts used by the workflow
│   │   ├── script.py
│   ├── notebooks
│   │   ├── notebook.py.ipynb
│   ├── report # see the report() function
│   │   ├── plot.rst
│   └── Snakefile
├── config
│   ├── README.md # a complete description of configuration options
│   ├── config.yaml
│   └── manifest.tsv
├── .test # a small test case that runs all rules in your workflow
│   ├── config.yaml
├── .github/workflows # yaml(s) for github actions (Continuous integration)
│   ├── main.yml
│   ├── lint.yml
│   ├── black.yml
├── .gitignore
├── .snakemake-workflow-catalog.yml # Specify required flags and options
└── results # results of the workflow
```

## **How** do I do this, it seems like a lot of work...

#### Don't worry I made it easy by making a template that can serve as the starting point for any Snakemake workflow

- [github.com/mrvollger/SmkTemplate](https://github.com/mrvollger/SmkTemplate)

#### If you are not experienced with **Snakemake** don't worry, it has excellent documentation and tutorials

- [Docs](https://snakemake.readthedocs.io/en/stable/)
- [Tutorial](https://snakemake.readthedocs.io/en/stable/tutorial/tutorial.html)

## Reasons **why** you should aim to make quality workflows

- A provably working Snakemake that is scalable, portable, and readable
- A website for your tool
  - [ \<user\>.github.io/\<workflow>](https://mrvollger.github.io/SmkTemplate/)
- Automated documentation and publication of your workflow on the Snakemake website
  - [snakemake.github.io/snakemake-workflow-catalog?usage=\<user>/\<workflow>](https://snakemake.github.io/snakemake-workflow-catalog?usage=mrvollger/SmkTemplate)
- You will be able to submit to journals like [JOSS](https://joss.readthedocs.io/en/latest/submitting.html) in about an hour
- You get these pretty badges!
  - [![Actions Status](https://github.com/mrvollger/SmkTemplate/workflows/CI/badge.svg)](https://github.com/mrvollger/SmkTemplate/actions) [![Actions Status](https://github.com/mrvollger/SmkTemplate/workflows/Linting/badge.svg)](https://github.com/mrvollger/SmkTemplate/actions) [![Actions Status](https://github.com/mrvollger/SmkTemplate/workflows/black/badge.svg)](https://github.com/mrvollger/SmkTemplate/actions)

## **Why** follow this guide/advice in particular?

- These recommendations are my attempt at a unified collection of standards suggested by the **Snakemake developers**

# Making a **readable** workflow

## Making your code beautiful and ready to share

#### Check that you follow Snakemake coding recommendations with

`snakemake --lint `

#### Format your snakemake consistently and automatically

`snakefmt .`

#### Format your python code consistently and automatically

`black .`

## What should and should not be in your rules

#### Should have

- Input and output
- Log file
- Environment declaration if using `shell` or `script`
- `resources` and `threads` if appropriate.

#### Should not have

- Any reference to a system specific resource e.g. `sge`,`grid`,`qsub`, `module load`, ect.
- Global python references e.g. `{SNAKEMAKE_DIR}`, add an option to the `params` declaration instead, or use wildcard references e.g. `{wildcards.sample}`

## Example rule

```python
rule RepeatMasker:
    input:
        fasta="a.fasta",
    output:
        out="a.out",
    resources:
        mem=1048, # in MB by default
    threads: 1
    conda:
        "envs/env.yml"
    log:
        "rm.out.log",
    params:
        species=config.get("RepeatMaskerSpecies", "human"),
    shell:
        """
        RepeatMasker -s -xsmall -e ncbi \
            -species {params.species} \
            -dir $(dirname {input.fasta}) \
            -pa {threads} \
            {input.fasta}  2> {log}
        """
```
