---
title: "AI モデルとデプロイメント"
slug: /ai-models
---

## AI モデルとは?

![AI Model](https://learn.microsoft.com/windows/ai/images/winml-model-flow.png)

AI モデル (または機械学習モデル)は、データセットで訓練されたプログラムで、_特定のパターンを認識_することができます。モデルの訓練は、AIが新しいデータを推論し、予測を行うために使用できる_アルゴリズム_を定義します。[🔖 | Learn more](https://learn.microsoft.com/windows/ai/windows-ml/what-is-a-machine-learning-model)  
   
## 大規模言語モデルとは？  
大規模言語モデル（LLM）は、多様なソースからの膨大なデータで訓練された、自然言語テキストを処理および生成できるAIの一種です。「基盤モデル」は、LLMの特定のインスタンスまたはバージョンを指します。これらのトピックについては、次のレッスンで詳しく説明します。[🔖 | Learn more](https://learn.microsoft.com/training/modules/introduction-large-language-models/)  
   
## 埋め込みとは？  
埋め込みとは、機械学習モデルやアルゴリズムがより簡単に使用できる**特別なデータ表現形式**です。これは、テキストデータの意味論的意味を_浮動小数点数のベクトル_として情報密度の高い表現を提供します。ベクトル空間における埋め込み間の距離は、元のテキスト入力間の意味的類似性に直接相関します。[🔖 | Learn more](https://learn.microsoft.com/azure/ai-services/openai/concepts/understand-embeddings#embedding-models)  
   
埋め込みは、テキストデータのより効率的なクエリのためにベクトル検索メソッドを使用するのに役立ちます。例えば、Azure Cosmos DB for MongoDB vCoreのようなデータベースでベクトル類似性検索を実行するのに役立ちます。現在推奨される埋め込みモデルは`text-embedding-ada-002`です。[🔖 | Learn more](https://learn.microsoft.com/azure/ai-services/openai/how-to/embeddings?tabs=console)  
   
## どのモデルを使用すべきか？  
モデルを選択する際には多くの考慮事項があります。  
- モデルの価格（トークン単位、アーティファクト単位）  
- モデルの可用性（バージョン、地域別）  
- モデルの性能（評価指標）  
- モデルの能力（機能とパラメータ）  
   
一般的なガイドとして、次のことをお勧めします：  
- **まずはgpt-35-turboから始めましょう。** このモデルは非常に経済的で、良好なパフォーマンスを持っています。OpenAIのChatGPTなどのチャットアプリケーションによく使用されますが、チャットや会話以外の幅広いタスクにも使用できます。  
- **4,096トークン以上を生成する必要がある場合や、大きなプロンプトをサポートする必要がある場合は、gpt-35-turbo-16k、gpt-4、またはgpt-4-32kに移行しましょう。** これらのモデルはより高価で、遅くなる可能性があり、可用性が限られていますが、現在最も強力なモデルです。*トークン化については後のレッスンで詳しく説明します。*  
- **埋め込み**を検索、クラスタリング、推薦、および異常検出などのタスクに考慮してください。  
- **DALL-E（プレビュー）を使用して**、ユーザーが提供するテキストプロンプトから画像を生成します。以前のモデルでは出力はテキスト（チャット）でしたが、今回は違います。  
- **Whisper（プレビュー）を使用して**、音声をテキストに変換するか、音声の書き起こしを行います。このモデルは英語の音声ファイルの書き起こしに最適化されて訓練されていますが、他の言語の音声も書き起こすことができます。モデルの出力は英語のテキストです。個々の音声ファイルを迅速に書き起こすため、または他の言語の音声を英語に翻訳するために使用できます - プロンプトに基づいたガイダンスを提供します。[🔖 | Learn more](https://learn.microsoft.com/azure/ai-services/openai/how-to/working-with-models?tabs=powershell)  
   
## Azure OpenAI (AOAI)とは？  
OpenAIには、ユーザーが提供する自然言語テキスト入力または**「プロンプト」**から異なる種類のコンテンツ（テキスト、画像、音声、コード）を「生成」できる[多様な言語モデル](https://platform.openai.com/docs/models/overview)があります。Azure OpenAIサービスは、これらのOpenAIモデルにREST APIを介してアクセスを提供します。[現在利用可能なモデル](https://learn.microsoft.com/en-us/azure/ai-services/openai/concepts/models)には、GPT-4、GPT-4 Turbo Preview、GPT-3.5、Embeddings、DALL-E（プレビュー）およびWhisper（プレビュー）が含まれます。Azure OpenAIは、基盤モデルのOpenAIの更新に合わせて、新しいバージョンを[定期的にリリース](https://learn.microsoft.com/azure/ai-services/openai/concepts/model-versions)しています。開発者は、プログラム（Python SDKを使用）またはブラウザ（Azure AI Studioを使用）を介してアクセスできます。[🔖 | Learn more](https://learn.microsoft.com/azure/ai-services/openai/overview).  
   
## ワークショップモデル展開  
:::info OUR AZURE PLAYGROUND  
このワークショップでは以下を行います：  
- **`gpt-35-turbo`モデルを使用** - チャット補完のため  
- **`gpt-4`モデルを議論** - 比較のため  
:::  
   
考慮すべき主な点は次の2つです：  
- [モデルバージョン](https://learn.microsoft.com/azure/ai-services/openai/concepts/models) - モデルは何を提供するのか？トレーニングのカットオフ＆リタイアメントの日付は？  
- [クォータと制限](https://learn.microsoft.com/azure/ai-services/openai/quotas-limits) - モデルはどの地域で利用可能か？モデルの使用制限は？  
   
以下は、注目する2つのモデルについてのデータの例です。他のモデルの詳細については、上記のリンクを参照してください。  
   
| モデル (バージョン) | 可用性 | リクエスト制限 | トレーニングデータ (まで) |  
|:---|:---|:---|:---|  
| [gpt-3.5-turbo (0613)](https://learn.microsoft.com/azure/ai-services/openai/concepts/models#gpt-35-models)| 10地域 | 4096トークン | 2021年9月 |  
| [gpt-4 (0613)](https://learn.microsoft.com/azure/ai-services/openai/concepts/models#gpt-4-and-gpt-4-turbo-preview-models)| 9地域 | 8192トークン | 2021年9月 |