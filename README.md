---
base_model: https://huggingface.co/budecosystem/genz-70b
inference: false
language:
- en
library_name: transformers
license: llama2
model_creator: Bud
model_name: GenZ 70B
model_type: llama
pipeline_tag: text-generation
prompt_template: '### User:

  {prompt}


  ### Assistant:

  '
quantized_by: TheBloke
---

<!-- header start -->
<!-- 200823 -->
<div style="width: auto; margin-left: auto; margin-right: auto">
<img src="https://i.imgur.com/EBdldam.jpg" alt="TheBlokeAI" style="width: 100%; min-width: 400px; display: block; margin: auto;">
</div>
<div style="display: flex; justify-content: space-between; width: 100%;">
    <div style="display: flex; flex-direction: column; align-items: flex-start;">
        <p style="margin-top: 0.5em; margin-bottom: 0em;"><a href="https://discord.gg/theblokeai">Chat & support: TheBloke's Discord server</a></p>
    </div>
    <div style="display: flex; flex-direction: column; align-items: flex-end;">
        <p style="margin-top: 0.5em; margin-bottom: 0em;"><a href="https://www.patreon.com/TheBlokeAI">Want to contribute? TheBloke's Patreon page</a></p>
    </div>
</div>
<div style="text-align:center; margin-top: 0em; margin-bottom: 0em"><p style="margin-top: 0.25em; margin-bottom: 0em;">TheBloke's LLM work is generously supported by a grant from <a href="https://a16z.com">andreessen horowitz (a16z)</a></p></div>
<hr style="margin-top: 1.0em; margin-bottom: 1.0em;">
<!-- header end -->

# GenZ 70B - GPTQ
- Model creator: [Bud](https://huggingface.co/budecosystem)
- Original model: [GenZ 70B](https://huggingface.co/budecosystem/genz-70b)

<!-- description start -->
## Description

This repo contains GPTQ model files for [Bud's GenZ 70B](https://huggingface.co/budecosystem/genz-70b).

Multiple GPTQ parameter permutations are provided; see Provided Files below for details of the options provided, their parameters, and the software used to create them.

<!-- description end -->
<!-- repositories-available start -->
## Repositories available

* [AWQ model(s) for GPU inference.](https://huggingface.co/TheBloke/Genz-70b-AWQ)
* [GPTQ models for GPU inference, with multiple quantisation parameter options.](https://huggingface.co/TheBloke/Genz-70b-GPTQ)
* [2, 3, 4, 5, 6 and 8-bit GGUF models for CPU+GPU inference](https://huggingface.co/TheBloke/Genz-70b-GGUF)
* [Bud's original unquantised fp16 model in pytorch format, for GPU inference and for further conversions](https://huggingface.co/budecosystem/genz-70b)
<!-- repositories-available end -->

<!-- prompt-template start -->
## Prompt template: User-Assistant-Newlines

```
### User:
{prompt}

### Assistant:

```

<!-- prompt-template end -->


<!-- README_GPTQ.md-provided-files start -->
## Provided files and GPTQ parameters

Multiple quantisation parameters are provided, to allow you to choose the best one for your hardware and requirements.

Each separate quant is in a different branch.  See below for instructions on fetching from different branches.

All recent GPTQ files are made with AutoGPTQ, and all files in non-main branches are made with AutoGPTQ. Files in the `main` branch which were uploaded before August 2023 were made with GPTQ-for-LLaMa.

<details>
  <summary>Explanation of GPTQ parameters</summary>

- Bits: The bit size of the quantised model.
- GS: GPTQ group size. Higher numbers use less VRAM, but have lower quantisation accuracy. "None" is the lowest possible value.
- Act Order: True or False. Also known as `desc_act`. True results in better quantisation accuracy. Some GPTQ clients have had issues with models that use Act Order plus Group Size, but this is generally resolved now.
- Damp %: A GPTQ parameter that affects how samples are processed for quantisation. 0.01 is default, but 0.1 results in slightly better accuracy.
- GPTQ dataset: The dataset used for quantisation. Using a dataset more appropriate to the model's training can improve quantisation accuracy. Note that the GPTQ dataset is not the same as the dataset used to train the model - please refer to the original model repo for details of the training dataset(s).
- Sequence Length: The length of the dataset sequences used for quantisation. Ideally this is the same as the model sequence length. For some very long sequence models (16+K), a lower sequence length may have to be used.  Note that a lower sequence length does not limit the sequence length of the quantised model. It only impacts the quantisation accuracy on longer inference sequences.
- ExLlama Compatibility: Whether this file can be loaded with ExLlama, which currently only supports Llama models in 4-bit.

</details>

| Branch | Bits | GS | Act Order | Damp % | GPTQ Dataset | Seq Len | Size | ExLlama | Desc |
| ------ | ---- | -- | --------- | ------ | ------------ | ------- | ---- | ------- | ---- |
| [main](https://huggingface.co/TheBloke/Genz-70b-GPTQ/tree/main) | 4 | 128 | Yes | 0.1 | [wikitext](https://huggingface.co/datasets/wikitext/viewer/wikitext-2-v1/test) | 4096 | 36.65 GB | Yes | 4-bit, with Act Order and group size 128g. Uses even less VRAM than 64g, but with slightly lower accuracy. | 
| [gptq-4bit-32g-actorder_True](https://huggingface.co/TheBloke/Genz-70b-GPTQ/tree/gptq-4bit-32g-actorder_True) | 4 | 32 | Yes | 0.1 | [wikitext](https://huggingface.co/datasets/wikitext/viewer/wikitext-2-v1/test) | 4096 | 40.66 GB | Yes | 4-bit, with Act Order and group size 32g. Gives highest possible inference quality, with maximum VRAM usage. | 
| [gptq-3bit--1g-actorder_True](https://huggingface.co/TheBloke/Genz-70b-GPTQ/tree/gptq-3bit--1g-actorder_True) | 3 | None | Yes | 0.1 | [wikitext](https://huggingface.co/datasets/wikitext/viewer/wikitext-2-v1/test) | 4096 | 26.77 GB | No | 3-bit, with Act Order and no group size. Lowest possible VRAM requirements. May be lower quality than 3-bit 128g. | 
| [gptq-3bit-128g-actorder_True](https://huggingface.co/TheBloke/Genz-70b-GPTQ/tree/gptq-3bit-128g-actorder_True) | 3 | 128 | Yes | 0.1 | [wikitext](https://huggingface.co/datasets/wikitext/viewer/wikitext-2-v1/test) | 4096 | 28.03 GB | No | 3-bit, with group size 128g and act-order. Higher quality than 128g-False. |

<!-- README_GPTQ.md-provided-files end -->

<!-- README_GPTQ.md-download-from-branches start -->
## How to download from branches

- In text-generation-webui, you can add `:branch` to the end of the download name, eg `TheBloke/Genz-70b-GPTQ:main`
- With Git, you can clone a branch with:
```
git clone --single-branch --branch main https://huggingface.co/TheBloke/Genz-70b-GPTQ
```
- In Python Transformers code, the branch is the `revision` parameter; see below.
<!-- README_GPTQ.md-download-from-branches end -->
<!-- README_GPTQ.md-text-generation-webui start -->
## How to easily download and use this model in [text-generation-webui](https://github.com/oobabooga/text-generation-webui).

Please make sure you're using the latest version of [text-generation-webui](https://github.com/oobabooga/text-generation-webui).

It is strongly recommended to use the text-generation-webui one-click-installers unless you're sure you know how to make a manual install.

1. Click the **Model tab**.
2. Under **Download custom model or LoRA**, enter `TheBloke/Genz-70b-GPTQ`.
  - To download from a specific branch, enter for example `TheBloke/Genz-70b-GPTQ:main`
  - see Provided Files above for the list of branches for each option.
3. Click **Download**.
4. The model will start downloading. Once it's finished it will say "Done".
5. In the top left, click the refresh icon next to **Model**.
6. In the **Model** dropdown, choose the model you just downloaded: `Genz-70b-GPTQ`
7. The model will automatically load, and is now ready for use!
8. If you want any custom settings, set them and then click **Save settings for this model** followed by **Reload the Model** in the top right.
  * Note that you do not need to and should not set manual GPTQ parameters any more. These are set automatically from the file `quantize_config.json`.
9. Once you're ready, click the **Text Generation tab** and enter a prompt to get started!
<!-- README_GPTQ.md-text-generation-webui end -->

<!-- README_GPTQ.md-use-from-python start -->
## How to use this GPTQ model from Python code

### Install the necessary packages

Requires: Transformers 4.32.0 or later, Optimum 1.12.0 or later, and AutoGPTQ 0.4.2 or later.

```shell
pip3 install transformers>=4.32.0 optimum>=1.12.0
pip3 install auto-gptq --extra-index-url https://huggingface.github.io/autogptq-index/whl/cu118/  # Use cu117 if on CUDA 11.7
```

If you have problems installing AutoGPTQ using the pre-built wheels, install it from source instead:

```shell
pip3 uninstall -y auto-gptq
git clone https://github.com/PanQiWei/AutoGPTQ
cd AutoGPTQ
pip3 install .
```

### For CodeLlama models only: you must use Transformers 4.33.0 or later.

If 4.33.0 is not yet released when you read this, you will need to install Transformers from source:
```shell
pip3 uninstall -y transformers
pip3 install git+https://github.com/huggingface/transformers.git
```

### You can then use the following code

```python
from transformers import AutoModelForCausalLM, AutoTokenizer, pipeline

model_name_or_path = "TheBloke/Genz-70b-GPTQ"
# To use a different branch, change revision
# For example: revision="main"
model = AutoModelForCausalLM.from_pretrained(model_name_or_path,
                                             device_map="auto",
                                             trust_remote_code=False,
                                             revision="main")

tokenizer = AutoTokenizer.from_pretrained(model_name_or_path, use_fast=True)

prompt = "Tell me about AI"
prompt_template=f'''### User:
{prompt}

### Assistant:

'''

print("\n\n*** Generate:")

input_ids = tokenizer(prompt_template, return_tensors='pt').input_ids.cuda()
output = model.generate(inputs=input_ids, temperature=0.7, do_sample=True, top_p=0.95, top_k=40, max_new_tokens=512)
print(tokenizer.decode(output[0]))

# Inference can also be done using transformers' pipeline

print("*** Pipeline:")
pipe = pipeline(
    "text-generation",
    model=model,
    tokenizer=tokenizer,
    max_new_tokens=512,
    do_sample=True,
    temperature=0.7,
    top_p=0.95,
    top_k=40,
    repetition_penalty=1.1
)

print(pipe(prompt_template)[0]['generated_text'])
```
<!-- README_GPTQ.md-use-from-python end -->

<!-- README_GPTQ.md-compatibility start -->
## Compatibility

The files provided are tested to work with AutoGPTQ, both via Transformers and using AutoGPTQ directly. They should also work with [Occ4m's GPTQ-for-LLaMa fork](https://github.com/0cc4m/KoboldAI).

[ExLlama](https://github.com/turboderp/exllama) is compatible with Llama models in 4-bit. Please see the Provided Files table above for per-file compatibility.

[Huggingface Text Generation Inference (TGI)](https://github.com/huggingface/text-generation-inference) is compatible with all GPTQ models.
<!-- README_GPTQ.md-compatibility end -->

<!-- footer start -->
<!-- 200823 -->
## Discord

For further support, and discussions on these models and AI in general, join us at:

[TheBloke AI's Discord server](https://discord.gg/theblokeai)

## Thanks, and how to contribute

Thanks to the [chirper.ai](https://chirper.ai) team!

Thanks to Clay from [gpus.llm-utils.org](llm-utils)!

I've had a lot of people ask if they can contribute. I enjoy providing models and helping people, and would love to be able to spend even more time doing it, as well as expanding into new projects like fine tuning/training.

If you're able and willing to contribute it will be most gratefully received and will help me to keep providing more models, and to start work on new AI projects.

Donaters will get priority support on any and all AI/LLM/model questions and requests, access to a private Discord room, plus other benefits.

* Patreon: https://patreon.com/TheBlokeAI
* Ko-Fi: https://ko-fi.com/TheBlokeAI

**Special thanks to**: Aemon Algiz.

**Patreon special mentions**: Alicia Loh, Stephen Murray, K, Ajan Kanaga, RoA, Magnesian, Deo Leter, Olakabola, Eugene Pentland, zynix, Deep Realms, Raymond Fosdick, Elijah Stavena, Iucharbius, Erik Bjäreholt, Luis Javier Navarrete Lozano, Nicholas, theTransient, John Detwiler, alfie_i, knownsqashed, Mano Prime, Willem Michiel, Enrico Ros, LangChain4j, OG, Michael Dempsey, Pierre Kircher, Pedro Madruga, James Bentley, Thomas Belote, Luke @flexchar, Leonard Tan, Johann-Peter Hartmann, Illia Dulskyi, Fen Risland, Chadd, S_X, Jeff Scroggin, Ken Nordquist, Sean Connelly, Artur Olbinski, Swaroop Kallakuri, Jack West, Ai Maven, David Ziegler, Russ Johnson, transmissions 11, John Villwock, Alps Aficionado, Clay Pascal, Viktor Bowallius, Subspace Studios, Rainer Wilmers, Trenton Dambrowitz, vamX, Michael Levine, 준교 김, Brandon Frisco, Kalila, Trailburnt, Randy H, Talal Aujan, Nathan Dryer, Vadim, 阿明, ReadyPlayerEmma, Tiffany J. Kim, George Stoitzev, Spencer Kim, Jerry Meng, Gabriel Tamborski, Cory Kujawski, Jeffrey Morgan, Spiking Neurons AB, Edmond Seymore, Alexandros Triantafyllidis, Lone Striker, Cap'n Zoog, Nikolai Manek, danny, ya boyyy, Derek Yates, usrbinkat, Mandus, TL, Nathan LeClaire, subjectnull, Imad Khwaja, webtim, Raven Klaugh, Asp the Wyvern, Gabriel Puliatti, Caitlyn Gatomon, Joseph William Delisle, Jonathan Leane, Luke Pendergrass, SuperWojo, Sebastain Graf, Will Dee, Fred von Graf, Andrey, Dan Guido, Daniel P. Andersen, Nitin Borwankar, Elle, Vitor Caleffi, biorpg, jjj, NimbleBox.ai, Pieter, Matthew Berman, terasurfer, Michael Davis, Alex, Stanislav Ovsiannikov


Thank you to all my generous patrons and donaters!

And thank you again to a16z for their generous grant.

<!-- footer end -->

# Original model card: Bud's GenZ 70B

---

<div align="center"><h1 align="center">~ GenZ ~</h1><img src="https://raw.githubusercontent.com/BudEcosystem/GenZ/main/assets/genz-logo.png" width=150></div>


<p align="center"><i>Democratizing access to LLMs for the open-source community.<br>Let's advance AI, together. </i></p>

---


## Introduction 🎉

Welcome to **GenZ**, an advanced Large Language Model (LLM) fine-tuned on the foundation of Meta's open-source Llama V2 70B parameter model. At Bud Ecosystem, we believe in the power of open-source collaboration to drive the advancement of technology at an accelerated pace. Our vision is to democratize access to fine-tuned LLMs, and to that end, we will be releasing a series of models across different parameter counts (7B, 13B, and 70B) and quantizations (32-bit and 4-bit) for the open-source community to use, enhance, and build upon. 

<p align="center"><img src="https://raw.githubusercontent.com/BudEcosystem/GenZ/main/assets/mt_bench_compare.png" width="500"></p>

The smaller quantization version of our models makes them more accessible, enabling their use even on personal computers. This opens up a world of possibilities for developers, researchers, and enthusiasts to experiment with these models and contribute to the collective advancement of language model technology. 

GenZ isn't just a powerful text generator—it's a sophisticated AI assistant, capable of understanding and responding to user prompts with high-quality responses. We've taken the robust capabilities of Llama V2 and fine-tuned them to offer a more user-focused experience. Whether you're seeking informative responses or engaging interactions, GenZ is designed to deliver.

And this isn't the end. It's just the beginning of a journey towards creating more advanced, more efficient, and more accessible language models. We invite you to join us on this exciting journey. 🚀

---

<h2>Milestone Releases ️🏁</h2>

**[21 August 2023]**
[_GenZ-70B_](https://huggingface.co/budecosystem/genz-70b) : We're excited to announce the release of our Genz 70BB model. Experience the advancements by downloading the model from [HuggingFace](https://huggingface.co/budecosystem/genz-70b).

**[27 July 2023]**
[_GenZ-13B V2 (ggml)_](https://huggingface.co/budecosystem/genz-13b-v2-ggml) : Announcing our GenZ-13B v2 with ggml. This variant of GenZ can run inferencing using only CPU and without the need of GPU. Download the model from [HuggingFace](https://huggingface.co/budecosystem/genz-13b-v2-ggml).

**[27 July 2023]**
[_GenZ-13B V2 (4-bit)_](https://huggingface.co/budecosystem/genz-13b-v2-4bit) : Announcing our GenZ-13B v2 with 4-bit quantisation. Enabling inferencing with much lesser GPU memory than the 32-bit variant. Download the model from [HuggingFace](https://huggingface.co/budecosystem/genz-13b-v2-4bit).

**[26 July 2023]**
[_GenZ-13B V2_](https://huggingface.co/budecosystem/genz-13b-v2) : We're excited to announce the release of our Genz 13B v2 model, a step forward with improved evaluation results compared to v1. Experience the advancements by downloading the model from [HuggingFace](https://huggingface.co/budecosystem/genz-13b-v2).

**[20 July 2023]**
[_GenZ-13B_](https://huggingface.co/budecosystem/genz-13b) : We marked an important milestone with the release of the Genz 13B model. The journey began here, and you can partake in it by downloading the model from [Hugging Face](https://huggingface.co/budecosystem/genz-13b).

---

<h2>Evaluations 🎯</h2>

Evaluating our model is a key part of our fine-tuning process. It helps us understand how our model is performing and how it stacks up against other models. Here's a look at some of the key evaluations for GenZ 70B:

<h3>Benchmark Comparison</h3>

We've compared GenZ models to understand the improvements our fine-tuning has achieved.

| Model Name | MT Bench | MMLU | Human Eval | BBH |
|:----------:|:--------:|:----:|:----------:|:----:|
| Genz 13B   | 6.12     | 53.62| 17.68      | 37.76|
| Genz 13B v2| 6.79     | 53.68| 21.95      | 38.1 |
| Genz 70B   | 7.33     | 70.32| 37.8       |54.69 |

<h3>MT Bench Score</h3>

A key evaluation metric we use is the MT Bench score. This score provides a comprehensive assessment of our model's performance across a range of tasks.

<p align="center"><img src="https://raw.githubusercontent.com/BudEcosystem/GenZ/main/assets/mt_bench_score.png" width="500"></p>


---

<h2>Getting Started on Hugging Face 🤗</h2>

Getting up and running with our models on Hugging Face is a breeze. Follow these steps:

<h3>1️⃣ : Import necessary modules</h3>


Start by importing the necessary modules from the ‘transformers’ library and ‘torch’.

```python
import torch
from transformers import AutoTokenizer, AutoModelForCausalLM

tokenizer = AutoTokenizer.from_pretrained("budecosystem/genz-70b", trust_remote_code=True)
model = AutoModelForCausalLM.from_pretrained("budecosystem/genz-70b", torch_dtype=torch.bfloat16, rope_scaling={"type": "dynamic", "factor": 2})

prompt = "### User:\nWrite a python flask code for login management\n\n### Assistant:\n"

inputs = tokenizer(prompt, return_tensors="pt")
sample = model.generate(**inputs, max_length=128)
print(tokenizer.decode(sample[0]))
```

Want to interact with the model in a more intuitive way? We have a Gradio interface set up for that. Head over to our GitHub page, clone the repository, and run the ‘generate.py’ script to try it out. Happy experimenting! 😄


<h2>Why Use GenZ? 💡</h2>


You might be wondering, "Why should I choose GenZ over a pretrained model?" The answer lies in the extra mile we've gone to fine-tune our models.

While pretrained models are undeniably powerful, GenZ brings something extra to the table. We've fine-tuned it with curated datasets, which means it has additional skills and capabilities beyond what a pretrained model can offer. Whether you need it for a simple task or a complex project, GenZ is up for the challenge.

What's more, we are committed to continuously enhancing GenZ. We believe in the power of constant learning and improvement. That's why we'll be regularly fine-tuning our models with various curated datasets to make them even better. Our goal is to reach the state of the art and beyond - and we're committed to staying the course until we get there.

But don't just take our word for it. We've provided detailed evaluations and performance details in a later section, so you can see the difference for yourself.

Choose GenZ and join us on this journey. Together, we can push the boundaries of what's possible with large language models.

---

<h2>Model Card for GenZ 70B 📄</h2>

Here's a quick overview of everything you need to know about GenZ 70B.

<h3>Model Details:</h3>


- Developed by: Bud Ecosystem
- Base pretrained model type: Llama V2 70B
- Model Architecture: GenZ 70B, fine-tuned on Llama V2 70B, is an auto-regressive language model that employs an optimized transformer architecture. The fine-tuning process for GenZ 70B leveraged Supervised Fine-Tuning (SFT)
- License: The model is available for commercial use under a custom commercial license. For more information, please visit: [Meta AI Model and Library Downloads](https://ai.meta.com/resources/models-and-libraries/llama-downloads/)

---

<h2>Intended Use 💼</h2>

When we created GenZ 70B, we had a clear vision of how it could be used to push the boundaries of what's possible with large language models. We also understand the importance of using such models responsibly. Here's a brief overview of the intended and out-of-scope uses for GenZ 70B.

<h3>Direct Use</h3>

GenZ 70B is designed to be a powerful tool for research on large language models. It's also an excellent foundation for further specialization and fine-tuning for specific use cases, such as:
- Text summarization
- Text generation
- Chatbot creation
- And much more!

<h3>Out-of-Scope Use 🚩</h3>

While GenZ 70B is versatile, there are certain uses that are out of scope:

- Production use without adequate assessment of risks and mitigation
- Any use cases which may be considered irresponsible or harmful
- Use in any manner that violates applicable laws or regulations, including trade compliance laws
- Use in any other way that is prohibited by the Acceptable Use Policy and Licensing Agreement for Llama 2

Remember, GenZ 70B, like any large language model, is trained on a large-scale corpora representative of the web, and therefore, may carry the stereotypes and biases commonly encountered online.

<h3>Recommendations 🧠</h3>

We recommend users of GenZ 70B to consider fine-tuning it for the specific set of tasks of interest. Appropriate precautions and guardrails should be taken for any production use. Using GenZ 70B responsibly is key to unlocking its full potential while maintaining a safe and respectful environment.

---

<h2>Training Details 📚</h2>

When fine-tuning GenZ 70B, we took a meticulous approach to ensure we were building on the solid base of the pretrained Llama V2 70B model in the most effective way. Here's a look at the key details of our training process:

<h3>Fine-Tuning Training Data</h3>

For the fine-tuning process, we used a carefully curated mix of datasets. These included data from OpenAssistant, an instruction fine-tuning dataset, and Thought Source for the Chain Of Thought (CoT) approach. This diverse mix of data sources helped us enhance the model's capabilities across a range of tasks.


<h3>Hyperparameters</h3>


Here are the hyperparameters we used for fine-tuning:

| Hyperparameter | Value |
| -------------- | ----- |
| Warmup Ratio | 0.04 |
| Learning Rate Scheduler Type | Cosine |
| Learning Rate | 2e-5 |
| Number of Training Epochs | 3 |
| Per Device Training Batch Size | 4 |
| Gradient Accumulation Steps | 4 |
| Precision | FP16 |
| Optimizer | AdamW |

---

<h2>Looking Ahead 👀</h2>

We're excited about the journey ahead with GenZ. We're committed to continuously improving and enhancing our models, and we're excited to see what the open-source community will build with them. We believe in the power of collaboration, and we can't wait to see what we can achieve together.

Remember, we're just getting started. This is just the beginning of a journey that we believe will revolutionize the world of large language models. We invite you to join us on this exciting journey. Together, we can push the boundaries of what's possible with AI. 🚀

---


Check the GitHub for the code -> [GenZ](https://raw.githubusercontent.com/BudEcosystem/GenZ)
