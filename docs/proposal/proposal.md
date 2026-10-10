# School of Computing &mdash; Year 4 Project Proposal Form

> Edit (then commit and push) this document to complete your proposal form.
> Make use of figures / diagrams where appropriate.
>
> Do not rename this file.

## SECTION A

|                     |                                               |
|---------------------|-----------------------------------------------|
|Project Title:       | LEEP - Literature-Extracted Enzyme Prediction |
|Student 1 Name:      | Theo Robin                                    |
|Student 1 ID:        | 23388446                                      |
|Student 2 Name:      | Bailey Scanlan                                |
|Student 2 ID:        | xxxxxxxx                                      |
|Project Supervisor:  | Luca Rossetto                                 |


## SECTION B

### Introduction

### Outline

LEEP will be a django-based web applicataion with a React frontend and will have two main functions: scientific literature extraction and enzyme prediction.

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

This idea was inspired by a company called Nuritas, who have done major work in bioactive peptide discovery and prediction. Their approach has found a novel way to speed up the process of identifying useful bioactive peptides in an area that will almost always have new things to discover. The company’s model inspired us to research other areas where a similar approach could be used, which is how we landed on enzymes.

The idea of this project is very similar in principle to how Nuritas has approached predicting useful bioactive peptides. You get your dataset, train your models, and then use the model to predict what could be useful for a specific scenario. In our case, this means learning from known enzyme-substrate relationships and using that information to predict which enzymes may be suitable for a target chemical transformation.

The challenge we found is that existing enzyme datasets are not always as complete as the information that exists in scientific literature. Many papers contain experiments that could potentially be used to enrich existing enzyme datasets with extra information, particularly experiments showing weak activity or no activity at all.

This is important because many existing enzyme-prediction approaches rely on synthetically generated negative examples when experimentally confirmed negative data is limited. These synthetic negatives are assumed examples of enzyme-substrate pairs that do not react, rather than results taken directly from experiments. Our literature-extraction process would allow us to recover more genuine experimental results, including successful, weak and unsuccessful reactions, and use these alongside existing curated enzyme data.

We can then compare models trained using genuine experimental negative results with models trained using synthetic negative examples, allowing us to investigate whether real experimental data improves enzyme prediction.

### Achievements

The end goal of the project is to help identify which enzymes may be capable of breaking down or transforming a given pollutant. For example, we may already know part of a degradation pathway:

A -> B (Pollutant A breaks down into B)
B -> C
C -> D

but there may be a later step where the required enzyme is unknown. LEEP would aim to use the experimental data gathered from scientific literature, alongside existing curated enzyme data, to rank enzymes that may be suitable for carrying out that missing transformation on:

D -> X?

Rather than attempting to test hundreds of thousands of possible enzymes, the aim is to narrow this search space down to a much smaller and more useful list of candidate enzymes for further experimental testing. The system will not prove that a predicted enzyme works, as this would require wet-lab validation, but it should help researchers prioritise which enzymes are most worth investigating.

The application will provide functions for uploading and processing scientific papers, reviewing and validating extracted enzyme experiments, storing these observations in a structured database, training and evaluating machine-learning models, and submitting a target transformation to receive a ranked list of candidate enzymes.

The users of LEEP would be relatively specialised and would mainly include researchers working in areas such as environmental biotechnology, bioinformatics, bioremediation and enzyme discovery. In particular, it could be useful for researchers investigating ways of breaking down pollutants or other difficult environmental compounds while reducing the number of candidates that need to be tested experimentally.

### Justification

Traditionally, identifying useful enzymes for a particular reaction can involve screening very large numbers of candidates, relying on enzymes already known in nature, or carrying out repeated experimental testing until something promising is found. This can make enzyme discovery slow, expensive and resource-intensive.

LEEP aims to speed up this process by using existing experimental knowledge and machine learning to narrow a very large search space down to a much smaller list of promising candidate enzymes. Instead of researchers having to investigate thousands or potentially hundreds of thousands of enzymes, the system would aim to prioritise those most likely to be useful for a target pollutant transformation.

This could be particularly useful in environmental biotechnology and bioremediation, where researchers may already understand part of how a pollutant breaks down but still need to identify an enzyme capable of carrying out a missing step in the pathway. By learning from both successful and unsuccessful past experiments, LEEP may help reduce unnecessary laboratory testing and allow researchers to focus time and resources on the most promising candidates.

The project could therefore be useful wherever enzyme discovery is limited by the size of the search space, with pollutant degradation being the main proof-of-concept application for LEEP.

### Programming language(s)

These are the planned programming languages:

- **Python** - Primary language for the Django backend, PDF processing, LLM fine-tuning and inference, machine learning, protein and chemical data processing, and data analysis.
- **JavaScript** - Used for frontend development, particularly through React and D3.js.
- **HTML/CSS** - Used for the structure and styling of the web interface.
- **SQL** - Used primarily through the Django ORM and PostgreSQL for querying and managing structured project data.

### Programming tools / Tech stack

These are the planned tools and technologies:

- **Django** - Main web application framework and backend.
- **React** - Frontend framework for building the interactive user interface.
- **D3.js** - Used for dashboard visualisation of extracted data, model performance and enzyme-ranking results.
- **PostgreSQL** - Relational database for papers, enzymes, substrates, experimental observations, validation records, model information and prediction results.
- **BRENDA** - Existing curated enzyme database used as a soruce of known enzyme, substrate, product, and activity information. LEEP will aim to enrich this tye of existing data using the extracted enzyme-substrate results from the literature.
- **PyMuPDF4LLM** - Used to extract and preprocess text and structured content from scientific PDF papers. **GROBID** may be considered as a fallback if more detailed scientific-document structure extraction is required.
- **Qwen3-4B** - Open-weight pretrained LLM used to extract structured enzyme experiment information from scientific text. The model may be adapted using supervised fine-tuning to improve performance on the specific enzyme-experiment extraction task.
- **Hugging Face Transformers, PEFT and TRL** - Used to load, fine-tune and evaluate the extraction model.
- **QLoRA** - Parameter-efficient fine-tuning method used to adapt the LLM while reducing GPU memory requirements by quantising the underlying model and training a relatively small set of adapter parameters.
- **ESM-2** - Pretrained protein language model accessed through Hugging Face and used to convert amino-acid sequences into numerical protein representations for the prediction model.
- **RDKit** - Used to process chemical structures and convert substrates into numerical molecular fingerprints suitable for machine-learning models.
- **XGBoost** - Primary machine-learning algorithm used to predict enzyme-substrate activity from protein and chemical representations.
- **Logistic Regression / Random Forest** - Potential baseline models used to compare the performance of the main XGBoost model.
- **scikit-learn** - Used for dataset splitting, preprocessing, baseline models, evaluation and performance metrics.
- **Pandas / NumPy** - Used for dataset preparation, cleaning, transformation and analysis.
- **Matplotlib** - Used primarily during exploratory data analysis and model evaluation. D3.js will be used for interactive visualisations within the final application.
- **Biopython** - May be used for handling biological sequence data, protein identifiers and related bioinformatics operations.
- **Jupyter Notebook** - Used for exploratory data analysis and machine-learning experimentation before models are integrated into the Django application.
- **Docker** - Used to create a reproducible development environment for the Django application, PostgreSQL database and associated dependencies.
- **uv** - Used for Python environment and dependency management.
- **DCU GitLab** - Used for version control, collaboration and CI/CD.

### Hardware

The project can be developed primarily on standard laptops or desktop computers. Access to a GPU may be useful for fine-tuning the language model and generating protein embeddings, particularly during experimentation. If required, we will look for suitable computing or GPU resources. No specialist physical hardware or laboratory equipment is required.

### Learning Challenges

> List the main new things (technologies, languages, tools, etc) that you will have to learn.


### System Architecture
> put diagram here Bailey

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
