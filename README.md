# Evaluating the Reproducibility of LLMs in Data Science

## Overview
To be added.

## Environment Setup
### Downloading Data
In the current folder, execute the script to download DiscoveryBench, QRData, and StatQA datasets by running:
   ```
   ./download_data.sh
   ```

### Using GPT-4o and o3-mini
1. Deploy the LLMs on [Azure](https://azure.microsoft.com/en-us/).
2. Create a `.env` file that includes the following keys:
   - `AZURE_OPENAI_API_KEY`
   - `AZURE_OPENAI_ENDPOINT`

### Using Claude-3.5-sonnet
1. Obtain access to LLMs on [Bedrock](https://aws.amazon.com/bedrock/).
2. Create a `.env` file that includes the following keys:
   - `AWS_ACCESS_KEY_ID`
   - `AWS_SECRET_ACCESS_KEY`
   - `AWS_DEFAULT_REGION`

### Using Llama-3.3 and DeepSeek-R1
1. Set Up the [Ollama](https://ollama.com/) Environment.
2. Edit the `/config/api_config.json` file and insert your host information (for example `http://127.0.0.1:11434`).

## Run Experiments
Execute the following command, replacing the placeholders as needed:
```
python -m experiments.run_experiment --dataset_name {dataset_name} --model_name {model_name} --agent_type {agent_type} --overwrite
```
- {dataset_name}: Choose from `DiscoveryBench`, `QRData`, or `StatQA`
- {model_name}: Choose from `gpt-4o`, `claude-3-5-sonnet`, or `o3-mini`
- {agent_type}: Choose from `COT`, `ROT`, `REFLEXION`, or `REACT` prompting strategies

**Note:** If you want to use `REFLEXION`, please make sure that you have already obtained the evaluation results for COT.

## Evaluation
Execute the following command, replacing the placeholders as needed:
```
python -m eval.run_reproducibility --dataset_name {dataset_name} --model_name {model_name} --agent_type {agent_type} --accuracy --reproducibility
```
- {dataset_name}: Choose from `DiscoveryBench`, `QRData`, or `StatQA`
- {model_name}: Choose from `gpt-4o`, `claude-3-5-sonnet`, or `o3-mini`
- {agent_type}: Choose from `COT`, `ROT`, `REFLEXION`, or `REACT` prompting strategies

**Note:** If you want to use `REFLEXION`, please make sure that you have already obtained the evaluation results for COT.

## Analysis
The results file will contain both accuracy and reproducibility metrics.
1. Accuracy: 
  - `1`: Accurate  
  - `0`: Inaccurate
2. Reproducibility:
  - `1`: Reproducible  
  - `0`: Irreproducible (with executable code)  
  - `-1`: Irreproducible (with non-executable code)

## Citation
To be added.
