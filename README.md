# Manubot manuscript repository: Protein k-mers enable assembly-free microbial metapangenomics

<!-- usage note: edit the H1 title above to personalize the manuscript -->

[![HTML Manuscript](https://img.shields.io/badge/manuscript-HTML-blue.svg)](https://dib-lab.github.io/2021-paper-metapangenomes/)
[![PDF Manuscript](https://img.shields.io/badge/manuscript-PDF-blue.svg)](https://dib-lab.github.io/2021-paper-metapangenomes/manuscript.pdf)
[![GitHub Actions Status](https://github.com/dib-lab/2021-paper-metapangenomes/workflows/Manubot/badge.svg)](https://github.com/dib-lab/2021-paper-metapangenomes/actions)

## Manuscript description

An estimated 2 billion species of microbes exist on Earth with orders of magnitude more strains. 
Microbial pangenomes are created by aggregating all genomes of a single clade and reflect the metabolic diversity of groups of organisms.
As *de novo* metagenome analysis techniques have matured and reference genome databases have expanded, metapangenome analysis has risen in popularity as a tool to organize the functional potential of organisms in relation to the environment from which those organisms were sampled.
However, the reliance on assembly and binning or on reference databases often leaves substantial portions of metagenomes unanalyzed, thereby underestimating the functional potential of a community.
To address this challenge, we present a method for metapangenomics that relies on amino acid k-mers (k~aa~-mers) and metagenome assembly graph queries.
To enable this method, we first show that k~aa~-mers estimate pangenome characteristics and that open reading frames can be accurately predicted from short shotgun sequencing reads using the previously developed tool orpheum.
These techniques enable pangenomics to be performed directly on short sequencing reads.
To enable metapangenome analysis, we combine these approaches with compact de Bruijn assembly graph queries to directly generate sets of sequencing reads for a specific species from a metagenome.
When applied to stool metagenomes from an individual receiving antibiotics over time, we show that these approaches identify strain fluctuations that coincide with antibiotic exposure.

## Manubot

<!-- usage note: do not edit this section -->

Manubot is a system for writing scholarly manuscripts via GitHub.
Manubot automates citations and references, versions manuscripts using git, and enables collaborative writing via GitHub.
An [overview manuscript](https://greenelab.github.io/meta-review/ "Open collaborative writing with Manubot") presents the benefits of collaborative writing with Manubot and its unique features.
The [rootstock repository](https://git.io/fhQH1) is a general purpose template for creating new Manubot instances, as detailed in [`SETUP.md`](SETUP.md).
See [`USAGE.md`](USAGE.md) for documentation how to write a manuscript.

Please open [an issue](https://git.io/fhQHM) for questions related to Manubot usage, bug reports, or general inquiries.

### Repository directories & files

The directories are as follows:

+ [`content`](content) contains the manuscript source, which includes markdown files as well as inputs for citations and references.
  See [`USAGE.md`](USAGE.md) for more information.
+ [`output`](output) contains the outputs (generated files) from Manubot including the resulting manuscripts.
  You should not edit these files manually, because they will get overwritten.
+ [`webpage`](webpage) is a directory meant to be rendered as a static webpage for viewing the HTML manuscript.
+ [`build`](build) contains commands and tools for building the manuscript.
+ [`ci`](ci) contains files necessary for deployment via continuous integration.

### Local execution

The easiest way to run Manubot is to use [continuous integration](#continuous-integration) to rebuild the manuscript when the content changes.
If you want to build a Manubot manuscript locally, install the [conda](https://conda.io) environment as described in [`build`](build).
Then, you can build the manuscript on POSIX systems by running the following commands from this root directory.

```sh
# Activate the manubot conda environment (assumes conda version >= 4.4)
conda activate manubot

# Build the manuscript, saving outputs to the output directory
bash build/build.sh

# At this point, the HTML & PDF outputs will have been created. The remaining
# commands are for serving the webpage to view the HTML manuscript locally.
# This is required to view local images in the HTML output.

# Configure the webpage directory
manubot webpage

# You can now open the manuscript webpage/index.html in a web browser.
# Alternatively, open a local webserver at http://localhost:8000/ with the
# following commands.
cd webpage
python -m http.server
```

Sometimes it's helpful to monitor the content directory and automatically rebuild the manuscript when a change is detected.
The following command, while running, will trigger both the `build.sh` script and `manubot webpage` command upon content changes:

```sh
bash build/autobuild.sh
```

### Continuous Integration

Whenever a pull request is opened, CI (continuous integration) will test whether the changes break the build process to generate a formatted manuscript.
The build process aims to detect common errors, such as invalid citations.
If your pull request build fails, see the CI logs for the cause of failure and revise your pull request accordingly.

When a commit to the `main` branch occurs (for example, when a pull request is merged), CI builds the manuscript and writes the results to the [`gh-pages`](https://github.com/dib-lab/2021-paper-metapangenomes/tree/gh-pages) and [`output`](https://github.com/dib-lab/2021-paper-metapangenomes/tree/output) branches.
The `gh-pages` branch uses [GitHub Pages](https://pages.github.com/) to host the following URLs:

+ **HTML manuscript** at https://dib-lab.github.io/2021-paper-metapangenomes/
+ **PDF manuscript** at https://dib-lab.github.io/2021-paper-metapangenomes/manuscript.pdf

For continuous integration configuration details, see [`.github/workflows/manubot.yaml`](.github/workflows/manubot.yaml).

## License

<!--
usage note: edit this section to change the license of your manuscript or source code changes to this repository.
We encourage users to openly license their manuscripts, which is the default as specified below.
-->

[![License: CC BY 4.0](https://img.shields.io/badge/License%20All-CC%20BY%204.0-lightgrey.svg)](http://creativecommons.org/licenses/by/4.0/)
[![License: CC0 1.0](https://img.shields.io/badge/License%20Parts-CC0%201.0-lightgrey.svg)](https://creativecommons.org/publicdomain/zero/1.0/)

Except when noted otherwise, the entirety of this repository is licensed under a CC BY 4.0 License ([`LICENSE.md`](LICENSE.md)), which allows reuse with attribution.
Please attribute by linking to https://github.com/dib-lab/2021-paper-metapangenomes.

Since CC BY is not ideal for code and data, certain repository components are also released under the CC0 1.0 public domain dedication ([`LICENSE-CC0.md`](LICENSE-CC0.md)).
All files matched by the following glob patterns are dual licensed under CC BY 4.0 and CC0 1.0:

+ `*.sh`
+ `*.py`
+ `*.yml` / `*.yaml`
+ `*.json`
+ `*.bib`
+ `*.tsv`
+ `.gitignore`

All other files are only available under CC BY 4.0, including:

+ `*.md`
+ `*.html`
+ `*.pdf`
+ `*.docx`

Please open [an issue](https://github.com/dib-lab/2021-paper-metapangenomes/issues) for any question related to licensing.
