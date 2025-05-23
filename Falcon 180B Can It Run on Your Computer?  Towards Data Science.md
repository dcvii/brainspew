---
title: "Falcon 180B: Can It Run on Your Computer? | Towards Data Science"
source: https://towardsdatascience.com/falcon-180b-can-it-run-on-your-computer-c3f3fb1611a9/
author:
  - "[[Benjamin Marie]]"
published: 2023-09-12
created: 2025-02-10
description: Yes, if you have enough CPU RAM
tags:
  - clippings
  - llm
---
In May 2023, The Technology Innovation Institute (TII) of Abu-Dhabi released two pre-trained LLMs: Falcon-7B and Falcon-40B, and their chat versions. These two models demonstrated very good performance and were ranked first on the [OpenLLM leaderboard](https://huggingface.co/spaces/HuggingFaceH4/open_llm_leaderboard).

A third model released by TII just joined the Falcon family: Falcon 180B, a 180 billion parameter model. It has 2.5 more parameters than Llama 2 70B and 4.5 more than Falcon-40B.

Here are some facts about Falcon 180B (source: [Falcon 180B model card](https://huggingface.co/tiiuae/falcon-180B)):

- Pre-trained on 3.5 trillion tokens ([RefinedWeb](https://huggingface.co/datasets/tiiuae/falcon-refinedweb))
- Distributed with an Apache 2.0 license
- Has a size of 360 GB
- Is ranked first (as of 11th September 2023) on the [OpenLLM leaderboard](https://huggingface.co/spaces/HuggingFaceH4/open_llm_leaderboard):

![Screenshot of the OpenLLM leaderboard (11th September 2023) - Image by the author](https://towardsdatascience.com/wp-content/uploads/2023/09/0DQprCvjiay904ove.png)

Screenshot of the OpenLLM leaderboard (11th September 2023) – Image by the author

There is also a chat version. The models are available on the Hugging Face hub:

- [Falcon 180B](https://huggingface.co/tiiuae/falcon-180B)
- [Falcon 180B Chat](https://huggingface.co/tiiuae/falcon-180B-chat)

Falcon 180B is completely free and state-of-the-art. But it’s also a huge model.

*Can it run on your computer?*

Unless your computer is ready for very intensive computing, it can’t run Falcon 180B out-of-the-box. You will need to upgrade your computer and use a quantized version of the model.

In this article, I explain how you can run Falcon-180B on consumer hardware. We will see that it can be reasonably affordable to run a 180 billion parameter model on a modern computer. I also discuss several techniques that help reduce the hardware requirements.

## Loading Falcon 180B on your computer: What do you need?

The first thing you need to know is that Falcon 180B has 180 billion parameters stored as bfloat16. A (b)float16 parameter is 2 bytes in memory.

When you load a model, the standard Pytorch pipeline works like this:

1. An empty model is created: 180B parameters \* 2 bytes = 360 GB
2. Load in memory its weights: 180B parameters \* 2 bytes = 360 GB
3. Load the weights loaded at step 2 in the empty model created at step 1
4. Move the model obtained at step 3 on the device for inference, e.g., a GPU

Step 1 and step 2 are the ones that consume memory. In total, you would need 720 GB of memory available. This can be CPU RAM, but for fast inference, you may want to use GPUs, e.g., 9 A100 with 80 GB of VRAM.

With either CPU RAM or VRAM, that’s a lot of memory. Fortunately, these requirements can be easily reduced.

On the Hugging Face Hub, Falcon 180B is distributed using the safetensors format. This format has several advantages over the standard Pytorch format. It (almost) does zero copy so the model is directly loaded into the empty model created at step 1. It saves a lot of memory.

> ***About safetensors***
> 
> *[safetensors](https://huggingface.co/docs/safetensors/index) saves memory but it also makes the model safer to run since no arbitrary code can be stored in this format. safetensors models are also much faster to load. Use this format instead of the ".bin" format when you download models from the hub for faster, safe, and memory-efficient loading.*

Even though it looks like we skip step 2, there is still some memory overhead to expect. TII wrote on [the model card](https://huggingface.co/tiiuae/falcon-180B) that 400 GB of memory would work. That’s still a lot but 220 GB less than using the standard Pytorch format.

We need a device with 400 GB, e.g., 5 A100 GPUs with 80 GB of VRAM. We are still far from a "consumer" configuration.

## Split Falcon 180B over multiple memory devices

You may not have a single memory device with 400 GB, but your computer has probably more than 400 GB of memory if you combine the memory of all the following devices:

- The GPUs VRAM: If you have an NVIDIA RTX 3090 or 4090, that’s already 24 GB.
- The CPU RAM: Most modern computers have at least 12 GB of CPU RAM. CPU RAM is also very cheap to extend.
- The hard drive (or SSD): That can be several terabytes of free memory. Note that an SSD (type NVMe M2) would be much faster than a typical hard drive if you plan to use it to run an LLM.

To take advantage of the devices available, we can split Falcon 180B so that it uses the maximum memory available of a device in this order of priority: GPU, CPU RAM, and hard drive.

This is easily achievable with [Accelerate](https://huggingface.co/docs/accelerate/index) device\_map.

device\_map puts entire layers of the model on the different devices that you have.

![device_map - Image by the author](https://towardsdatascience.com/wp-content/uploads/2023/09/0NmOIQsFmiofIwLuY.jpg)

device\_map – Image by the author

If you want to see some examples of device\_map usage, [check my notebooks](https://kaitchup.substack.com/p/notebooks). I use device\_map in most of them.

[device\_map is very convenient to avoid CUDA out-of-memory errors](https://kaitchup.substack.com/p/device-map-avoid-out-of-memory-errors-when-running-large-language-models-af7de5076f9d). But still far from ideal if you plan to use Falcon 180B on consumer hardware. Even with a high-end configuration with 24 GB of VRAM and 32 GB of CPU RAM, it would leave several hundred GBs on the hard drive.

This is an issue for two reasons:

- hard drives and SSDs are much **slower than VRAM and CPU RAM**. Loading and running Falcon 180B from a hard drive would take a very long time.
- consumer hard drives and SSDs were **not designed and tested for this kind of intensive use**. If many parts of the model are offloaded on the hard drive, the system would have to access and read the huge splits of the models many times during inference. It’s a huge number of reading operations for a prolonged time. If you do inference for days, e.g., to generate some synthetic datasets, that may break your hard drive or at least significantly reduce its life expectancy.

To avoid overusing the hard drive, we don’t have many solutions:

- Add one more GPU: Most high-end motherboards can hold two RTX 3090/4090. It would give you 48 GB of VRAM.
- Extend the CPU RAM: Most motherboards have 4 slots available for CPU RAM kits. Kits of 4\*128GB CPU RAM are sold but not easy to find and are still expensive. *Note: There is also a limit on the total amount of CPU RAM that your OS can support. For Windows 10, it’s 2 TB. If you have an older OS you should have a look at its documentation before buying more RAM.*
- Quantize Falcon 180B and extend the CPU RAM.

The quantization of Falcon 180B is one of the best options to reduce its memory consumption.

## Reduce the size of Falcon 180B with quantization

It’s now common practice to quantize very [Large Language Models](https://towardsdatascience.com/tag/large-language-models/ "Large Language Models") to a lower precision. [GPTQ](https://arxiv.org/abs/2210.17323) and [bitsandbytes nf4](https://arxiv.org/abs/2305.14314) are two popular ways to quantize LLM to 4-bit precision.

Falcon 180B uses bfloat16. We saw that it’s 360 GB.

Once quantized to 4-bit precision, it’s only 90 GB (180 billion parameters \* 0.5 Bytes). We can load the 4-bit Falcon 180B with 100 GB of memory (90GB + some memory overhead).

If you have 24 GB of VRAM, you "only" need 75 GB of CPU RAM. It is still a lot but much more affordable than loading the original model, and it wouldn’t offload layers of the models on the hard drive during inference. *Note: You still need 100 GB of free space on the hard drive to store the model.*

You don’t even need a GPU. With 128 GB of CPU RAM, you could do inference using only your CPU.

The quantization itself is extremely costly. Thankfully, we can already find quantized versions online. [TheBloke](https://huggingface.co/TheBloke) released 4-bit versions made with GPTQ:

- [4-bit Falcon 180B](https://huggingface.co/TheBloke/Falcon-180B-GPTQ)
- [4-bit Faclon 180B Chat](https://huggingface.co/TheBloke/Falcon-180B-Chat-GPTQ)

*Note: There are also 3-bit models available as "branches" of the models. Follow the instructions from the 4-bit model cards to get them.*

While the precision of the model is reduced, the performance of the model remains similar according to [Hugging Face’s experiments](https://huggingface.co/blog/falcon-180b).

GPTQ models are fast for inference and you can fine-tune them with LoRA adapters. For instance, I show how to fine-tune Llama 2 quantized with GPTQ in this article:

> [**Quantize and Fine-tune LLMs with GPTQ Using Transformers and TRL**](https://kaitchup.substack.com/p/quantize-and-fine-tune-llms-with)

While it’s possible to fine-tune GPTQ models, I don’t recommend it. Fine-tuning with QLoRA has a similar memory consumption but yields better models thanks to the better quantization with nf4 as shown in the [QLoRA paper](https://arxiv.org/abs/2305.14314).

## Conclusion

To sum up, you need quantization and 100 GB of memory to run Falcon 180B on a reasonably affordable computer.

For fast inference or fine-tuning, you will need a GPU. The RTX 4090 (or the RTX 3090 24GB, which is more affordable but slower) would be enough to load 1/4 of the quantized model. If you have enough space in your computer case, you could even put two RTX cards.

If you want to run Falcon-180B on a CPU-only configuration, i.e., without a GPU, forget about fine-tuning, it would be too slow. Inference would also be slow but with a recent high-end CPU and software optimized for faster inference, such as llama.cpp, running Falcon 180B is possible.

If you are interested in using [llama.cpp](https://github.com/ggerganov/llama.cpp) have a look at my article explaining how to run Vicuna using only the CPU:

> [**High-Speed Inference with llama.cpp and Vicuna on CPU**](https://kaitchup.substack.com/p/high-speed-inference-with-llama-cpp-and-vicuna-on-cpu-136d28e7887b)