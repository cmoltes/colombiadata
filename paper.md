---
title: 'verdata: An R package for analyzing data from the Truth Commission in Colombia'
tags:
    - R
    - missing data
    - capture-recapture
    - multiple systems estimation
    - multiple imputation
    - Colombia
    - conflict

authors:
    - name: Maria Gargiulo
      orcid: 0000-0003-1870-8990
      euqal-contrib: true
      corresponding: true
      affiliation: 1
    - name: María Juliana Durán
      orcid: 0009-0005-3720-8125
      equal-contrib: true
      affiliation: 1
    - name: Paula Andrea Amado
      orcid: 0009-0004-0806-0857
      equal-contrib: true
      affiliation: 1
    - name: Patrick Ball
      affiliation: 1
affiliations:
    - name: Human Rights Data Analysis Group
      index: 1
date: 16 August 2023
bibliography: paper.bib
---

# Summary

In 2016, the Colombian Government and the guerrilla group *Fuerzas Armadas Revolucionarias de Colombia – Ejército del Pueblo* (FARC-EP) signed a peace agreement ending decades of hostilities between the two groups. As part of the agreement, the *Comisión para el Esclarecimiento de la Verdad, la Convivencia y la No Repetición* (CEV; hereafter the Truth Commission) was created, a temporary institution charged with investigating what happened during the armed conflict, clarifying violations of international humanitarian law, and explaining the conflict in all its complexity to Colombian society. As part of the truth and reconciliation process, the Truth Commission collaborated with the *Jurisdicción Especial para la Paz* (JEP), a temporary judicial body, and the Human Rights Data Analysis Group (HRDAG) to produce official statistics about the magnitudes and patterns of five human rights violations---forced displacement, enforced disappearance, homicide, kidnapping, and forced recruitment of minors [@amado2022]. These analyses made use of over 100 databases compiled by over 40 organizations, including governmental institutions, civil society organizations, and victims' collectives.

The data compiled by the joint JEP-CEV-HRDAG project are publicly available from the [*Departamento Administrativo Nacional de Estadística* (DANE)](https://microdatos.dane.gov.co/index.php/catalog/795).  The data published by DANE is available in a format that may not be familiar to researchers who have not previously worked with statistical imputation methods. Recognizing this, `verdata` was created support researchers in responsibly and correctly using the data despite the potential unfamiliarity of its structure. Researchers can use `verdata` to verify that the data files they are using in their analyses have not been altered, to replicate the main findings of the technical appendix, and to design new analyses of the conflict in Colombia.

# Statement of need

Collecting data on human rights abuses in conflict settings is a difficult and often dangerous task. Organizations collecting such data may have constrained resources, lack physical access to areas where violence is occurring, or may be unable to collect data due to security concerns or community mistrust, among other challenges [e.g., @gargiulo2022; @price2014; @price2015]. As a result, the data produced by these data collection efforts is seldom a complete enumeration of all violence that occurred nor a statistically representative sample. Furthermore, instances of violence that are documented may be missing key information about victims, perpetrators, or contextual details about the violent events. The incompleteness of the data is not a critique of the data itself nor the organizations that courageously document human rights violations, but rather it is an empirical reality that must be addressed in quantitative work analyzing conflict-related violence.

The data analyzed in the joint JEP-CEV-HRDAG project was no exception to this empirical reality and was subject to two types of missing data: missing fields and underreporting. Related to missing fields, some records were missing socio-demographic information about victims such as their age, sex, or ethnicity, information identifying armed groups thought to be responsible for the violence, or precise information about the date and location of a particular violent event. These gaps in the data pose challenges for analyses seeking to stratify the data based on any fields containing missing values. With respect to underreporting, some instances of violence were not documented by any of the databases we received, leaving some victims' stories untold [@amado2022]. Moreover, this missingness is unlikely to be randomly distributed among members of the victim population, meaning that inferences drawn from samples of documented victims alone could result in erroneous conclusions about patterns of violence.

The joint JEP-CEV-HRDAG project employed two statistical methods to address the two types of missingness. To address missing fields within records of documented victims, the project used the `R` package `mice` [@vanbuuren2011] to perform multiple imputation [e.g., @murray2018], probabilistically filling in missing values at the record level multiple times. Multiple systems estimation [e.g., @bird2018; @chao2001], performed on the imputed replicate files, was then used to estimate the number of missing observations, that is, the number of the victims never documented by any of the data sources used in the project.[^mse] To estimate the number of missing observations, we used a Bayesian latent class multiple-capture model [@manriquevallier2016] implemented in the `R` package `LCMCR`. The analyses presented in the technical appendix of the joint project combine these two methods to examine patterns of enforced disappearance, homicide, kidnapping, and forced recruitment of minors in the armed conflict.[^displacement]

[^mse]: Multiple systems estimation is also called capture-recapture in some disciplines.

[^displacement]: While the join JEP-CEV-HRDAG project also examined forced displacement due to the armed conflict, we were unable to provide multiple systems estimation estimates of forced displacements because nearly all documented victims were registered on only one list, the *Registro Único de Víctimas*. As a result, we did not have sufficient overlap with other sources to construct estimates using multiple systems estimation, which generally requires three or more sources in the case of applications to human rights questions.

DANE has published 100 imputed replicate files with missing values filled in at the record level available for each of these four violations. This data format where there is no single file representing "the data" may be unfamiliar to researchers who have not worked with multiple imputation methods in the past and researchers may be tempted to select a single imputed replicate file to conduct their analyses rather than computing their analyses on multiple replicate files and combining the results using standard practices based on the laws of total expectation and total variance. The `verdata` package aims to support researchers in using the data from the Colombian Truth Commission responsibly and correctly despite the potential unfamiliarity of its structure. Software packages have not historically been created to facilitate the access and use of data published by past truth commissions. To date, the `pinochet` package [@freire2019], which facilitates access to data about killings and disappearances published in the Chilean Truth Commission, is the only other example of a software package created for this purpose.

To complement the package, we have also created a [repository](https://github.com/HRDAG/verdata-examples) of examples of basic function use, replications of main findings from the technical appendix, and applications to other studies of interest not examined in the technical appendix. We have also published a series of pre-calculated estimates that researchers can opt to use to reduce the computational costs of multiple systems estimation. These pre-calculated estimates are available from the Colombian Truth Commission [website](http://comisiondelaverdad.co/analitica-de-datos-informacion-y-recursos#c3).

We hope that `verdata` will play a role in expanding the use of statistical methods to address the two types of missing data in research on the conflict in Colombia, and armed conflicts more generally, so that the statistical biases apparent in individual data sources are not reproduced in future research on the conflict.

# Acknowledgements

We thank Tarak Shah, Valentina Rozo-Angel, and Dr. Megan Price for their helpful comments and Micaela Morales for her thoughtful beta testing.

Support for this project was provided by the British Embassy in Colombia Conflict, Stability and Security Fund, the Swiss Embassy in Colombia, Human Security Division, Justus Liebig University Gießen, with funds awarded by the German Foreign Federal Office, and Filecoin Foundation for the Decentralized Web.

# References

<!-- done -->
