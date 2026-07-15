
# AISec 2026 Submission #116 - Reproducibility Materials

This repository accompanies our paper submitted to AISec 2026 (submission #116). We provide these materials to enable reviewers to verify our results and reproduce our analyses.

---

## Overview  
The repository includes:  
1. **Source Code**: Implementation of the combined deep learning and machine learning architecture for payload analysis and classification.  
2. **Trained Models**: Pre-trained models for replicating our classification results are available on [zenodo](https://zenodo.org/records/21360582).
3. **Supplementary Scripts**: Tools for data preprocessing, analysis, and visualization.  
4. **Docker Setup**: A containerized environment to execute the fuzzers on the provided APIs, enabling to replicate or generate the dataset independently.  
5. **Dataset**: To preserve anonymity, representative OpenAPI specifications are provided for all five APIs, in place of the payload dataset used to train the models.

---

## Purpose of the Docker Setup  
The Docker container is designed to streamline the execution of fuzzers against the five custom APIs developed for our study. This setup can be used for:  
- **Reproducing Results**: The users can replicate the dataset used in the paper by executing the fuzzers with the provided scripts.  
- **Generating New Data**: The container allows the users to regenerate the entire dataset or customize the fuzzing process for their own experimentation.  

The APIs, built following the OpenAPI specification, represent diverse scenarios, including CRUD operations, OAuth2 flows, and IoT interactions, enabling evaluation of fuzzing techniques.  

---

## How to Use the Docker Setup  

### Step 1: Build the Docker Image  
```bash
cd path/to/docker_fuzzer-identifier
docker buildx build --platform linux/amd64 -t image_fuzzer-identifier:1.0.0 .
```
_Note: Ensure to include the **.** (dot) at the end of the command._

### Step 2: Save and Load the Docker Image  
Save the image:
```bash
docker save -o image_fuzzer-identifier.img image_fuzzer-identifier:1.0.0
```
Load the saved image:
```bash
docker load -i path/to/docker_fuzzer-identifier/image_fuzzer-identifier.img
```

### Step 3: Run the Docker Container  
Run the container while mounting the data directory:
```bash
docker run -v path/to/docker_fuzzer-identifier/data:/docker_fuzzer-identifier/data --name container_fuzzer-identifier -d image_fuzzer-identifier:1.0.0
```
_e.g._  
```bash
docker run -v D:/ag/github/fuzzing/docker_fuzzer-identifier/data:/docker_fuzzer-identifier/data --name container_fuzzer-identifier -d image_fuzzer-identifier:1.0.0
```

### Step 4: Access the Docker Container  
Attach to the running container for executing bash commands:
```bash
docker exec -it container_fuzzer-identifier bash
```

---

## Running Fuzzers Iteratively  

### Bash Scripts for Iterative Execution  
The following scripts execute each fuzzer iteratively on the APIs:  
- **APIFuzzer**: `/docker_fuzzer-identifier/scripts/bash_script_to_run_APIFuzzer_Iteratively.sh`  
- **Kiterunner**: `/docker_fuzzer-identifier/scripts/bash_script_to_run_Kiterunner_Iteratively.sh`  
- **RESTler**: `/docker_fuzzer-identifier/scripts/bash_script_to_run_RESTler.sh`  
  _Note: RESTler provides an in-built time-setting functionality._  
- **Schemathesis**: `/docker_fuzzer-identifier/scripts/bash_script_to_run_Schemathesis_Iteratively.sh`  

---

If you have any questions, please do not hesitate to contact the authors.

---
