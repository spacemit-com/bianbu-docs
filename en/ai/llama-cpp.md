---
sidebar_position: 4
---

# llama.cpp

llama.cpp is an open source inference framework written in pure C/C++. It is designed to enable large language models in GGUF/GGML format such as Llama to run quickly on local CPU/GPU (laptop, mobile phone, `muse pi` or even browser) without relying on heavyweight frameworks.

## Installation

Download the compressed file `spacemit-llama.cpp` and unzip it

```bash
wget https://archive.spacemit.com/spacemit-ai/llama.cpp/spacemit-llama.cpp.riscv64.0.0.4.tar.gz -P ~/
tar -xzvf ~/spacemit-llama.cpp.riscv64.0.0.4.tar.gz -C ~/
```

## Download model

spacemit-llama.cpp currently supports accelerating models in three quantization formats: Q4_K_M, Q4_0, and Q4_1.   
Here is an example to illustrate how to use it quickly:

```bash
wget https://modelscope.cn/models/unsloth/Qwen3-0.6B-GGUF/resolve/master/Qwen3-0.6B-Q4_0.gguf -P ～/
```

Import environment

```bash
export LD_LIBRARY_PATH=/home/bianbu/spacemit-llama.cpp.riscv64.0.0.4/lib
```

## Usage

```bash
cd ~/spacemit-llama.cpp.riscv64.0.0.4/bin
./llama-cli -m ~/Qwen3-0.6B-Q4_0.gguf --threads 4
```

![](../static/llama-cpp.png)

## API usage

Execute the command to start the llama.cpp service:
```bash
cd ~/spacemit-llama.cpp.riscv64.0.0.4/bin
./llama-server --port 9090 -m ~/Qwen3-0.6B-Q4_0.gguf --threads 4
```

### Browser usage

Search `http://localhost:9090` in the browser to open the llama server and use llama.cpp directly in the browser

![](../static/llama-serve.png)

### Local API Requests

For example:
```bash
curl -X POST http://127.0.0.1:9090/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
        "model": "Qwen3-0.6B",
        "messages": [
          { "role": "user", "content": "介绍一下自己" }
        ],
        "stream": false
      }'
```

![](../static/llama-api.png)