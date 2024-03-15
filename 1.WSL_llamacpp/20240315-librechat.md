# WindowsでLLM
# LibreChat編

Chat UIでローカルChatGPTっぽい環境を構築する。UIは[LibreChat](https://github.com/danny-avila/LibreChat)を使用し、llama-cpp-pythonサーバのLLMに接続する手順。  

## はじめに
- [LibreChat](https://github.com/danny-avila/LibreChat)は、ChatGPTに似たWeb UIの実装。
- かなり多機能ため、シンプルにllama-cpp-pythonサーバと接続するための手順。
- [WSL/llama-cpp-python編](https://github.com/cellhone/WinLLM/tree/main/1.WSL_llamacpp)で、WSL、llama-cpp-pythonの環境が構築済みであること


```
git clone https://github.com/danny-avila/LibreChat.git
cd LibreChat
cp .env.example  .env ## 設定ファイル
```

`vi .env`
```
ENDPOINTS=openAI
PROXY=
OPENAI_API_KEY=None
#DEBUG_OPENAI=true ## 必要に応じて

OPENAI_MODELS=gpt-3.5-turbo
OPENAI_TITLE_MODEL=gpt-3.5-turbo
OPENAI_REVERSE_PROXY=http://host.docker.internal:8080 ## Dockeのコンテナなので
```