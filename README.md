# AIRepr: An Analyst-Inspector Framework for Evaluating Reproducibility of LLMs in Data Science
Official repository for the paper ''_AIRepr: An Analyst-Inspector Framework for Evaluating Reproducibility of LLMs in Data Science_''
![Alt text](Figures/human_in_loop_overview.png)

## Overview
Large language models (LLMs) are increasingly used to automate data analysis through executable code generation.  Yet, data science tasks often admit multiple statistically valid solutions, e.g. different modeling strategies, making it critical to understand the reasoning behind analyses, not just their outcomes. While manual review of LLM-generated code can help ensure statistical soundness, it is labor-intensive and requires expertise. A more scalable approach is to evaluate the underlying workflows—the logical plans guiding code generation. However, it remains unclear how to assess whether a LLM-generated workflow supports reproducible implementations.

To address this, we present AIRepr, an **A**nalyst–**I**nspector framework for automatically evaluating and improving the **repr**oducibility of LLM-generated data analysis workflows. Our framework is grounded in statistical principles and supports scalable, automated assessment. We introduce two novel reproducibility-enhancing prompting strategies and benchmark them against standard prompting across 15 analyst–inspector LLM pairs and 1,032 tasks from three public benchmarks. Our findings show that workflows with higher reproducibility also yield more accurate analyses, and that reproducibility-enhancing prompts substantially improve both metrics. This work provides a foundation for more transparent, reliable, and efficient human–AI collaboration in data science. 
![Alt text](Figures/framework_overview.png)

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

## Experiments
Execute the following command, replacing the placeholders as needed:
```
python -m experiments.run_experiment --dataset_name {dataset_name} --model_name {model_name} --agent_type {agent_type} --overwrite
```
- {dataset_name}: Choose from `DiscoveryBench`, `QRData`, or `StatQA`
- {model_name}: Choose from `llama-3.3`, `deepseek-r1`, `gpt-4o`, `claude-3-5-sonnet`, or `o3-mini`
- {agent_type}: Choose from `COT`, `ROT`, `REFLEXION`, or `REACT` prompting strategies

**Note:** When using `REFLEXION`, please make sure that you have already obtained the evaluation results for COT.

## Evaluation
Execute the following command, replacing the placeholders as needed:
```
python -m eval.run_reproducibility --dataset_name {dataset_name} --model_name {model_name} --agent_type {agent_type} --accuracy --reproducibility
```
- {dataset_name}: Choose from `DiscoveryBench`, `QRData`, or `StatQA`
- {model_name}: Choose from `llama-3.3`, `deepseek-r1`, `gpt-4o`, `claude-3-5-sonnet`, or `o3-mini`
- {agent_type}: Choose from `COT`, `ROT`, `REFLEXION`, or `REACT` prompting strategies

**Note:** When using `REFLEXION`, please make sure that you have already obtained the evaluation results for COT.

## Analysis
The result file will contain both the accuracy and reproducibility metrics.
1. Accuracy: 
  - `1`: Accurate  
  - `0`: Inaccurate
2. Reproducibility:
  - `1`: Reproducible  
  - `0`: Irreproducible (reproduciblity=0 with executable code in the paper)  
  - `-1`: Irreproducible (reproduciblity=0 with inexecutable code in the paper)

## Citation
To be added.
