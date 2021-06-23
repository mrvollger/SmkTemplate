---
marp: true
theme: defualt
auto-scaling: true   
size: 4:3
paginate: true
footer: "
[![Twitter URL](https://img.shields.io/twitter/follow/mrvollger?color=blue&label=twitter&style=for-the-badge)](https://twitter.com/mrvollger)
[![Github badge](https://img.shields.io/github/stars/mrvollger?label=github&style=for-the-badge)](https://github.com/mrvollger)
[![Website](https://img.shields.io/website?down_color=gray&style=for-the-badge&up_color=blue&url=https%3A%2F%2Fmrvollger.github.io%2F)](https://mrvollger.github.io)
"
---

<style >section { font-size: 22px; }</style>
<style>
footer {
    height: 10px;
}
footer img {
    height: 20px;
    float: center;
 }
</style>

# Creating publication quality workflows with **Snakemake** and **Github**

#### Mitchell .R Vollger

---

# **Who** is this for?

#### Consider using this guide if you plan to do any of the following with a workflow

- **Reuse** the workflow in the future
- **Share** the workflow with anyone
- **Publish** the workflow

---

# **What** is a publication quality workflow

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

---

# **How** do I do this, it seems like a lot of work...

#### Don't worry I made it easy by making a template that can serve as the starting point for any Snakemake workflow

- [**https://github.com/mrvollger/SmkTemplate**](https://github.com/mrvollger/SmkTemplate)

#### If you are not experienced with **Snakemake** don't worry, it has excellent documentation and tutorials

- [**Docs**](https://snakemake.readthedocs.io/en/stable/)
- [**Tutorial**](https://snakemake.readthedocs.io/en/stable/tutorial/tutorial.html)

---

# **Why** follow this guide

#### If you follow this guide you will get the following things with relatively little effort

- Provably working Snakemake that is scalable, portable, and readable
- A website for your tool
  - [<user>.github.io/<workflow>](https://mrvollger.github.io/SmkTemplate/)
- Automated documentation and publication of your workflow on the Snakemake website
  - [snakemake.github.io/snakemake-workflow-catalog?usage=<user>/<workflow>](https://snakemake.github.io/snakemake-workflow-catalog?usage=mrvollger/SmkTemplate)
- Those pretty badges!
  - [![Actions Status](https://github.com/mrvollger/SmkTemplate/workflows/CI/badge.svg)](https://github.com/mrvollger/SmkTemplate/actions) [![Actions Status](https://github.com/mrvollger/SmkTemplate/workflows/Linting/badge.svg)](https://github.com/mrvollger/SmkTemplate/actions) [![Actions Status](https://github.com/mrvollger/SmkTemplate/workflows/black/badge.svg)](https://github.com/mrvollger/SmkTemplate/actions)

#### **Why** should I follow your advice?

- These recommendations are my attempt at a unified collection of standards suggested by the **Snakemake** developers

---
