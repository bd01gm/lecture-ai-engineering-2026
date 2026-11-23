# 第6回 解答

## 演習

<!-- [tool call] の行は、表示された行をそのまま貼り付けてください。終わらなかった STEP は、空欄のままでかまいません。 -->

- STEP 1 のツールの名前：
  ``` 
  search_materials,glossary_search_glossary 
- STEP 2 の [tool call]：  
  ```
   [tool call] glossary_search_glossary({'query': '3レベル'})  
   [tool return] glossary_search_glossary -> [{"term": "宿題の3レベル", "lecture": 1, "definition": "AIE2026の宿題の構成。「基礎（講義内容の確認）」「実装（自分でコードを書く）」「発展（調査や試行）」の3段階があり、どれか1つに取り組…  
    [usage] 入力 715 tokens / 出力 135 tokens / モデル応答 2 回 
- STEP 3 の [tool call]：  
   ```
   [tool call]   fetch_fetch({'url': 'https://modelcontextprotocol.io/'})  
   [tool return] fetch_fetch -> Contents of https://modelcontextprotocol.io/:
    ## Documentation Index
    Fetch the complete documentation index at: http…  
   [usage] 入力 2,181 tokens / 出力 110 tokens / モデル応答 2 回 
- STEP 4 の [tool call]
    ```
   [tool call]   aws_aws___search_documentation({'search_phrase': 'Amazon S3 versioning overview'})
  [tool return] aws_aws___search_documentation -> {'content': {'result': [{'rank_order': 1, 'title': 'Amazon S3 FAQs', 'context': '#### What is Versioning?\n\nVersioning …
  [usage] 入力 6,353 tokens / 出力 88 tokens / モデル応答 2 回  

- 気づき・疑問：  
Step4のｐ外部で動くサーバーに接続についてのjsonの記載が、前の2つと比べて非常にシンプル  

## 宿題

<!-- 基礎・実装・発展のどれか1つに取り組めば完了です。 -->

- 取り組んだレベル：基礎
- やったこと：  
1. app/mcp_server.pyの31行目に以下を追加 
   ```
    # TODO(宿題・基礎): get_lecture_summary も公開しよう
    server.tool()(tools.get_lecture_summary) 
2. 以下コマンドを実行 
   ```
   uv run python -m app.mcp_agent --list-tools
   uv run python -m app.mcp_agent --trace "第3回では何を学ぶ？"
- 結果：  
   ```
  [tool call]   glossary_get_lecture_summary({'lecture': 3})
  [tool return] glossary_get_lecture_summary -> # 第3回 AIエージェント

  ## この回のねらい

  - AIエージェントの基本構造が「モデル＋ループ＋ツール」であることを理解する
  - Pydantic AIで、ツールを使う学習支援エージェントを自分で作り、動かす

  ## 要点

  1.…
  [usage] 入力 5,862 tokens / 出力 246 tokens / モデル応答 2 回

- 気づき・疑問：  
コマンドないでツールを指定しなくても、質問からモデルが適切なツールを選定している
