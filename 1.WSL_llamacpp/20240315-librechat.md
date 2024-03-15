# WindowsでLLM
# LibreChat編

Chat UIでローカルChatGPTっぽい環境を構築する。  
UIは[LibreChat](https://github.com/danny-avila/LibreChat)を使用し、llama-cpp-pythonサーバのLLMに接続する手順。  

## はじめに
- [LibreChat](https://github.com/danny-avila/LibreChat)は、ChatGPTに似たWeb UIの実装。
- かなり多機能ため、シンプルにllama-cpp-pythonサーバと接続するための手順。
- [WSL/llama-cpp-python編](https://github.com/cellhone/WinLLM/tree/main/1.WSL_llamacpp)で、WSL、llama-cpp-pythonの環境が構築済みであること


## LibeChat

### インストール
```
git clone https://github.com/danny-avila/LibreChat.git
cd LibreChat
cp .env.example .env ## 設定ファイル
```

`.env`を修正する。  
以下のパラメータをセットする。
```
ENDPOINTS=openAI
PROXY=
OPENAI_API_KEY=None
#DEBUG_OPENAI=true ## 必要に応じて

OPENAI_MODELS=gpt-3.5-turbo
OPENAI_TITLE_MODEL=gpt-3.5-turbo
OPENAI_REVERSE_PROXY=http://host.docker.internal:8080 ## Dockeのコンテナなので
```

### 起動

```
docker compose up
```
Dockerで3つのプロセスが走る。
- librechat: 1.42GB
- mongo: 756MB
- meilisearch: 147MB
  
### Web UIにアクセスする

`http://localhost:3080/`

#### 初期アカウント作成
`Don't have an account? Sign up`  
初回アカウントを作る

### 停止
```
docker compose down
```

`^C`でも止まるが、Docker終了プロセスは残る。
```
docker ps --all
docker rm
```


## 課題
- LLMの回答終了後もCPU負荷が下がらない  
  負荷が下がるまで入力できない。  
  LibreChatが何かしてる？    原因不明（調査中）  
- チャットを続けると、どんどん遅くなっていく  
  Chat APIは過去の履歴を含んで問い合わせるため、質問文が長くなっていき、処理量が増大していくため。

<hr>
LLM実行委員会