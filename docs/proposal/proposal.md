# School of Computing &mdash; Year 4 Project Proposal Form

> Edit (then commit and push) this document to complete your proposal form.
> Make use of figures / diagrams where appropriate.
>
> Do not rename this file.

## SECTION A

|                     |                                               |
|---------------------|-----------------------------------------------|
|Project Title:       | LEAP - Literature-Extracted Enzyme Prediction |
|Student 1 Name:      | Theo Robin                                    |
|Student 1 ID:        | 23388446                                      |
|Student 2 Name:      | Bailey Scanlan                                |
|Student 2 ID:        | xxxxxxxx                                      |
|Project Supervisor:  | Luca Rossetto                                 |


## SECTION B

> Guidance: This document is expected to be approximately 3 pages in length, but it can exceed this page limit.
> It is also permissible to carry forward content from this proposal to your later documents (e.g. functional
> specification) as appropriate.
>
> Your proposal must include *at least* the following sections.


### Introduction

> Describe the general area covered by the project.

### Outline

LEAP will be a django-based web applicataion with a React frontend and will have two main functions: scientific literature extraction and enzyme prediction.

The first part of the system will allow researchers to upload or select scientific papers in PDF form. The text will be extracted and preprocessed before being passed to a fine-tuned LLM, which will identify reported enzyme experiments and extract relevant information. This is expected to inlcude:

- Enzyme
- Substrate
- Product, where known
- Activitu result, such as active, weak activity or inactive
- Assay conditions
- Supporting evidence

The final extraction schema may be refined as the project develops and the available literature is investigated. The LLM output will be converted into structured records and presented through a humanr review process, where extracted records can be approved, edited or rejected. Approved records will then be stored in PostgreSQL.

The validated literature data will be combined with suitable existing curated enzyme data where available to create a dataset for machine learning experiments. Protein sequences will be converted into numerical representations using a pretrained protein model, while chemical substrates will be represented using RDKit molecular fingerprints. These representations will be used to train an XGBoost model to predict the likelihood of activity between an enzyme and a substrate

A key part will be comparing models trained using genuine experimental negative results recovered from literature with models trained using synthetically generated negative examples. This will allow us to investigate whether real unsuccessful experiments improve enzyme prediction.

The final system will allow a researcher to specify a target chemical transformation and recieve a ranked list of candidate enzymes considered most suitable for further experimental testing. A dashboard will visualise the extracted dataset, LLM extraction performance, machine learning results and cadidate enzyme rankings.

### Background

> Where did the ideas come from?

### Achievements

> What functions will the project provide? Who will the users be?

### Justification

> Why/when/where/how will it be useful?

### Programming language(s)

> List the proposed language(s) to be used.

### Programming tools / Tech stack

> Describe the compiler, database, web server, etc., and any other software tools you plan to use.

### Hardware

If available, since there will be a lot of training may need extra resources with CPU Power.

### Learning Challenges

> List the main new things (technologies, languages, tools, etc) that you will have to learn.

### Breakdown of work

> Clearly identify who will undertake which parts of the project.
>
> It must be clear from the explanation of this breakdown of work both that each student is responsible for
> separate, clearly-defined tasks, and that those responsibilities substantially cover all of the work required
> for the project.




#### Student 1

> *Student 1 should complete this section.*

#### Student 2

> *Student 2 should complete this section.*


### Risk Register

> You are to complete a risk register to demonstrate how you will account for the potential risks (i.e. something going wrong) when you are working on your project. 
> The purpose of a risk register is to identify potential issues beforehand and plan mitigation strategies to ensure the success of the project. 
> The risks are different for each project by some examples include 

> if you are using physical components (e.g. sensors), what happens if they never arrive, or if they break, or if they are not suitable?
> if you are creating an AI/ML method , what happens if there is no suitable training data, or if the model performs poorly after training? 

| Description | Likelyhood | Severity | Mitigation |
|-------------|------------|----------|------------|
|             |            |          |            |
|             |            |          |            |
|             |            |          |            |
