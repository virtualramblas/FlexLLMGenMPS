# FlexLLMGen: High-throughput Generative Inference of Large Language Models with a Single GPU [[paper](https://arxiv.org/abs/2303.06865)]

FlexLLMGen is a high-throughput generation engine for running large language models with limited GPU memory. FlexLLMGen allows **high-throughput** generation by IO-efficient offloading, compression, and **large effective batch sizes**. This repo is a port of FlexLLMGen to Apple Silicon (M1/M2) GPU, as the [original work](https://github.com/FMInference/FlexLLMGen) supports only NVIDIA GPUs.  

## Motivation

In recent years, large language models (LLMs) have shown great performance across a 
wide range of tasks. Increasingly, LLMs have been applied not only to interactive 
applications (such as chat), but also to many "back-of-house" tasks.
These tasks include benchmarking, information extraction, data wrangling, and form processing.

One key characteristic of these applications is that they are **throughput-oriented**: they require
running LLM inferences over millions of tokens in batches, e.g., all the private documents in a company's
corpus, or all the tasks in the [HELM](https://crfm.stanford.edu/helm/latest/) benchmark.
These workloads are less sensitive to latency - the user starts up a job and lets it run overnight -
but increasing throughput is critical for reducing costs.
Throughput is a measure of tokens processed per second over the job's entire runtime (which can be hours).
Throughput-oriented workloads provide opportunities to trade off latency for higher throughput, which
makes it easier to take advantage of low-cost commodity GPUs. 

The goal of FlexLLMGen is to create a high-throughput system to enable new and exciting applications of 
foundation models to throughput-oriented tasks on low-cost hardware, such as a single commodity GPU
instead of expensive systems.  

❌ **Limitation**. As an offloading-based system running on weak GPUs, FlexLLMGen also has its limitations.
FlexLLMGen can be significantly slower than the case when you have enough powerful GPUs to hold the whole model, especially for small-batch cases.
FlexLLMGen is mostly optimized for throughput-oriented batch processing settings (e.g., classifying or extracting information from many documents in batches), on single GPUs.  
## Installation
From source:  
```
git clone https://github.com/virtualramblas/FlexLLMGenMPS.git
cd FlexLLMGenMPS
pip install -e .
```
