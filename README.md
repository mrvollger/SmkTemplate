# \<your workflow name\>

[![Actions Status](https://github.com/mrvollger/SmkTemplate/workflows/CI/badge.svg)](https://github.com/mrvollger/SmkTemplate/actions)

This is a Snakemake project template. The `Snakefile` is under `workflow`.

[Slides](https://mrvollger.github.io/SmkTemplate/slides) describing and justifying the use of this template.

## Install

Please start by installing [pixi](https://pixi.sh/latest/) which handles the environment of this Snakemake workflow.

You can then install the `pixi` environment by cloning this repository and running:

```bash
pixi install
```

## Usage

`pixi` handles the execution of the Snakemake workflows:

```bash
pixi run snakemake ...
```

And if you want to run this Snakemake from another directory you can do so with:

```bash
pixi run --manifest-path /path/to/snakemake/pixi.toml snakemake ...
```

where you update `/path/to/snakemake/pixi.toml` to the path of the `pixi.toml` you cloned.

And in place of `...` use all the normal Snakemake arguments for your workflow.
