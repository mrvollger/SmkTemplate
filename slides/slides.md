---
marp: true
theme: defualt
size: 4:3
paginate: true
footer: "
[![Twitter URL](https://img.shields.io/twitter/follow/mrvollger?color=blue&label=twitter&style=for-the-badge)](https://twitter.com/mrvollger)
[![Github badge](https://img.shields.io/github/stars/mrvollger?label=github&style=for-the-badge)](https://github.com/mrvollger)
[![Website](https://img.shields.io/website?down_color=gray&style=for-the-badge&up_color=blue&url=https%3A%2F%2Fmrvollger.github.io%2F)](https://mrvollger.github.io)
"
---

<style>
footer {
    height: 10px;
}
footer img {
    height: 20px;
    float: center;
 }
</style>

# Creating publication quality workflows with Snakemake and Github

---

# Publication quality workflows

- who
- what
  - documenting things
- why
- how

---

# Continuous integration and Github actions

```
.github/workflows/*.yml
```

---

# Snakemake layout

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
└── results # results of the workflow
```

---
