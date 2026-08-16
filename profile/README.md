<p align="center">
  <img src="assets/chimangoscan-logo-alpha.png" alt="ChimangoScan" width="520">
</p>

<p align="center">
  <b>Large-scale security measurement of the Docker Hub image ecosystem.</b><br>
  Built at <a href="https://ai-horizon-labs.github.io/">AI Horizon Labs</a>.
</p>

Docker Hub is where most containerized software is distributed from, and almost nobody
measures it at scale. The studies that exist tend to sample the popular images and to trust a
single scanner. ChimangoScan is the pipeline we built to do it properly: enumerate the
namespace, decide which images actually matter, scan them with several independent tools, and
publish the data rather than only the conclusions.

The core idea is an *exposure* score. An image matters not only for its own pull count but for
the pulls of every image that inherits its layers, so we reconstruct the layer graph and rank
by inherited weight. That is what makes it possible to cover most of the ecosystem's real
usage without scanning all of it.

## What the measurement covers

| | |
|---|---|
| Repositories crawled | 12.7 million |
| Images scanned | 52,895, the highest-exposure ones |
| Share of recorded pulls they represent | 84.7% of 663.8 billion |
| Scanners | six independent open-source tools |
| Findings collected | 170.4 million |
| Data released | 283 GB |

One result is worth stating on its own, because it decides how the rest should be read: the
measured security posture depends heavily on which tool you use. Of the distinct
vulnerabilities the three vulnerability scanners find, only 2.7% are reported by all three and
66.8% by a single one. Any single-scanner census is measuring its scanner as much as it is
measuring Docker Hub.

Two findings from the companion studies are worth carrying here. Posture is not driven by how
popular or how large an image is, but by the distribution it comes from and by its age. And
about one in twelve images ever published can no longer be pulled by a current Docker, because
its manifest schema is too old.

## Repositories

<table>
<tr>
<td width="300" valign="middle">
<a href="https://github.com/ChimangoScan/scanners"><img src="assets/preview-scanners.png" alt="scanners" width="280"></a>
</td>
<td valign="middle">
<a href="https://github.com/ChimangoScan/scanners"><b>scanners</b></a><br>
The tool. It runs a battery of container-security scanners over a list of images, on one machine or many, and consolidates every finding into a single schema. The picture is the finding that justifies it: one crate, six lamps, six different shadows.
</td>
</tr>
<tr>
<td width="300" valign="middle">
<a href="https://github.com/ChimangoScan/chimangoscan"><img src="assets/preview-chimangoscan.png" alt="chimangoscan" width="280"></a>
</td>
<td valign="middle">
<a href="https://github.com/ChimangoScan/chimangoscan"><b>chimangoscan</b></a><br>
<i>Vulnerabilities, Secrets and Misconfiguration in the Highest-Exposure Docker Hub Images</i>, the 12.7 million repository study (<a href="https://arxiv.org/abs/2608.02669">arXiv:2608.02669</a>).
</td>
</tr>
<tr>
<td width="300" valign="middle">
<a href="https://github.com/ChimangoScan/os-census"><img src="assets/preview-os-census.png" alt="os-census" width="280"></a>
</td>
<td valign="middle">
<a href="https://github.com/ChimangoScan/os-census"><b>os-census</b></a><br>
<i>A Multi-Scanner Census of the Linux Operating-System Base Images of Docker Hub</i>, SBSeg 2026. Every container starts from an OS base image: 5,606 of them, across 20 repositories, scanned with 14 tools. Whatever is wrong at the bottom repeats in everything built on top.
</td>
</tr>
<tr>
<td width="300" valign="middle">
<a href="https://github.com/ChimangoScan/chimango-baseline"><img src="assets/preview-chimango-baseline.png" alt="chimango-baseline" width="280"></a>
</td>
<td valign="middle">
<a href="https://github.com/ChimangoScan/chimango-baseline"><b>chimango-baseline</b></a><br>
<i>A Uniform Random-Sample Security Measurement of Docker Hub Images</i>, SBSeg 2026. What the typical image looks like, from 2,879 drawn uniformly at random across the whole registry rather than from the tall pile everyone measures.
</td>
</tr>
</table>

Each artifact repository carries the pipeline configuration, the corpus definition and the
scripts that regenerate every number, figure and table of its paper, so a reader can recompute
a result instead of trusting it.

## The paper page

The highest-exposure study has a page of its own, with the mechanism, the numbers and the PDF.

<p align="center">
  <a href="https://chimangoscan.github.io/chimangoscan-page/">
    <img src="assets/chimangoscan-page.png" alt="Project page of the highest-exposure Docker Hub study" width="720">
  </a>
</p>

## People

We work at [AI Horizon Labs](https://ai-horizon-labs.github.io/), a research group on
artificial intelligence and software engineering at the Universidade Federal do Pampa
(UNIPAMPA), on the Alegrete campus in Rio Grande do Sul, Brazil.

<table>
<tr>
<td width="140" valign="top" align="center">
<a href="https://github.com/CristhianKapelinski"><img src="https://github.com/CristhianKapelinski.png?size=200" width="120" alt="Cristhian Kapelinski"></a>
</td>
<td valign="top">
<b>CRISTHIAN KAPELINSKI</b> works on security, privacy, and machine learning at AI Horizon Labs, Universidade Federal do Pampa (UNIPAMPA). He built the measurement pipeline behind this organization, from the crawl of the Docker Hub namespace to the layer graph and the multi-scanner runs. His interests include privacy and memorization in language models, their use in security operations and the attacks against them, and large-scale measurement of software ecosystems.
<br><br>
<a href="https://orcid.org/0009-0005-5750-022X">ORCID</a> ·
<a href="http://lattes.cnpq.br/0100277568164430">Lattes</a> ·
<a href="https://scholar.google.com/citations?user=lV1lq-0AAAAJ">Scholar</a> ·
<a href="https://github.com/CristhianKapelinski">GitHub</a> ·
<a href="https://www.linkedin.com/in/cristhiankapelinski">LinkedIn</a>
</td>
</tr>
<tr>
<td width="140" valign="top" align="center">
<a href="https://github.com/inari18"><img src="https://github.com/inari18.png?size=200" width="120" alt="Beatriz Machado"></a>
</td>
<td valign="top">
<b>BEATRIZ MACHADO</b> works on cybersecurity research at AI Horizon Labs, Universidade Federal do Pampa (UNIPAMPA), on vulnerability analysis, data anonymization, and the use of language models to automate security work. She was a research fellow with the Brazilian National Research and Education Network (RNP), and wrote MulitaMiner, which turns the heterogeneous reports of security scanners into structured records with the help of language models. That work received second place for best paper at WRSeg 2025.
<br><br>
<a href="https://orcid.org/0009-0002-2750-0323">ORCID</a> ·
<a href="http://lattes.cnpq.br/6591374203213574">Lattes</a> ·
<a href="https://github.com/inari18">GitHub</a> ·
<a href="https://www.linkedin.com/in/beatriz18/">LinkedIn</a>
</td>
</tr>
<tr>
<td width="140" valign="top" align="center">
<a href="https://github.com/diegokreutz"><img src="https://github.com/diegokreutz.png?size=200" width="120" alt="Diego Kreutz"></a>
</td>
<td valign="top">
<b>DIEGO KREUTZ</b> received the B.S. degree in computer science and the M.Sc. degrees in production engineering and in informatics from the Universidade Federal de Santa Maria (UFSM), and the Ph.D. degree in computing. He has been a professor and researcher with the Universidade Federal do Pampa (UNIPAMPA) since 2008, where he coordinates the group, and has also carried out research at the University of Lisbon, the University of Luxembourg and Monash University. His interests include cybersecurity and adversarial AI, language models, AutoML, distributed systems and networks, and software artifact engineering.
<br><br>
<a href="https://orcid.org/0000-0003-0830-0238">ORCID</a> ·
<a href="http://lattes.cnpq.br/2781747995973774">Lattes</a> ·
<a href="https://scholar.google.com/citations?user=JcL8biEAAAAJ">Scholar</a> ·
<a href="https://github.com/diegokreutz">GitHub</a> ·
<a href="https://www.linkedin.com/in/diegokreutz/">LinkedIn</a>
</td>
</tr>
</table>

Lattes is the Brazilian national registry of researcher CVs, maintained by CNPq, the federal
research council.

## The name

A *chimango* is a caracara of the Pampa, the grasslands of southern Brazil. It is the bird that
circles a field slowly and misses nothing, which is roughly the job description.

## Citing

Each repository carries a `CITATION.cff` and a citation section at the end of its README. Cite
the paper the artifact belongs to rather than the repository URL alone.
