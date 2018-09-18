---
title: "CDvist"
date: 2015-12-02T10:28:18-05:00
draft: False
web: "http://cdvist.adebalilab.org"
---


![CDvist](/images/cdvist_logo.png)

CDvist (Comprehensive Domain Visualization Tool) is designed to sensitively identify protein domains of a given primary protein sequence.

## Pipeline

A given protein sequence is matched to domain models using high-specificity tools and only then unmatched segments are subjected to more sensitive algorithms resulting in a best possible comprehensive coverage.

### HMMER3

CDvist takes the advantage of HMMER3 version 3.1b2 and uses the hmmscan command to obtain specific Pfam domain hits. 

### RPS-BLAST

We use RPS-BLAST as the second choice of obtaining the specific hits after HMMER3. Unlike HMMER, RPS-BLAST uses PSSMs (Position Specific Score Matrix) rather than HMMs. The cutoff to decide whether the hit is true or not is selected by the "bit-score" cutoff determined by the CDD (Conserved Domain Database).

### HHsearch

HHsearch yields more sensitive domain assignments due to the fact that it uses profile-to-profile comparisons. In order to have a profile out of a single protein sequence, we first need to retrieve "similar" sequences and build a profile which should represent the original single query. We use HHblits to perform homology search on a database (like uniprot 20) having representative sequences only.

### CDvist

By default CDvist starts with HMMER3 search against PFAM database. Because default PFAM search with HMMER results in specific domain assignments, CDvist is confident about those so that we assign the significant hits directly to the query sequence. After HMMER3 (if selected), we start using "subsequence-based" search. This method slices the orphan subsequences and applies the following search only to the subsequence. If "significant" is found on the first subsequence, the first hit is assigned and the remaining "sub-sub-sequences" are retrieved iteratively until either the subsequence length is shorter than the "Gap Length" cutoff (default 30 aa) or no significant hit is found.

Subsequence-based search is especially useful for HHblits + HHsearch step as we build the profile (with HHblits) based on the subsequence rather than the entire protein sequence (if protein sequence had any assignments before). This step potentially removes a bias of domain-context as domains are evolutionary and functionally independent units.

## Frequently Asked Questions

### What is CDvist?

CDvist (Comprehensive Domain Visualization Tool) is a protein domain-searching webserver specialized in maximizing domain coverage of multidomain protein sequences.

### Why is CDvist needed?

The identification of protein domains is a key feature of protein sequence analysis. Several databases, notably Pfam (Punta et al., 2012), Simple Modular Architecture Research Tool (SMART) (Letunic et al., 2009), Clusters of Orthologous Groups (COG) (Tatusov et al., 2003), Conserved Domain Database (CDD) (Marchler-Bauer et al., 2013) and others, develop and maintain domain models. Searching tools such as RPS-BLAST (Marchler-Bauer et al., 2013), HMMER3 (Eddy, 2011) and HHpred/HHsearch (Hildebrand et al., 2009; Soding, 2005) are used to match sequences to domain models present in a given database. The size of the protein sequence database grows dramatically, whereas its coverage by pre-computed domain models increases very slowly (Rekapalli et al., 2012). Consequently, sensitive domain searches of sequences in bulk are necessary to improve computational coverage of the current and future protein sequence space. Despite the overwhelming success of the current state-of-the-art domain searching resources, three areas require further improvements: (i) combining tools with high specificity and tools with high sensitivity in a single framework, (ii) multiple query searches using highly sensitive (e.g. profile-to-profile) methods, (iii) visualization of most relevant information in a responsive and interactive way. **CDvist addresses these three issues.**

### Why are the results from CDvist and HHpred not identical?

Although they are usually similar, for sure not identical most of the time. The reason lies in the CDvist's subsequence-based search method. The HHpred application also allows for manual subsequence search iteratively on their website, CDvist automates this step.

### Can I run CDvist standalone?

As long as you have can run Docker, yes! The package is dockerized as the environment is not easy to setup out of a container. Please follow the instructions to install CDvist on your local machine. OS (Linux, Mac, Windows) shouldn't matter. Please note that Windows has not been tested yet.

### Can I serve CDvist?

Yes! Please do. If you have resources we would be happy to have a mirror site. We can provide technical support if needed.

### What is different in the latest version?

The pipeline of the first release of CDvist (1.0) ran on an HPC. However, since the HPC used was decommissioned, now we transferred the application to our local server which is not an HPC. The advantage is, as long as the resources are available (meaning not many CDvist jobs are running when you submit your job), your job starts running immediately without waiting for the queue. The disadvantage is the fact that the protein sequences do not run in parallel but sequential, which causes jobs to be completed in a longer time. We compensate the slowness issue by increasing the CPU and memory allocations for job submissions. Averagely a protein sequence is completed within a minute, meaning that your batch request of 500 proteins is expected to be completed within few hours after it starts. Not too bad.

