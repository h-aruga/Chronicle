# Chronicle: エージェント行動記録プロファイル (Draft v0.1)

本ドキュメントは、自律型AIエージェントの行動をxAPI規格に基づき構造化するためのプロファイル定義のドラフトです。エージェントが「何を考え、どう動き、どのような結果を得たか」を統一的に記録することを目的とします。

## 1. Verb（動詞）の定義

エージェントのワークフローにおける主要な行動を以下のVerbで定義します。

| Verb (動詞) | 意味 | 記録のタイミング |
| :--- | :--- | :--- |
| **Delegated** | 指示受領 | ユーザーや他のシステム（MCP等）からタスクを割り当てられた時。 |
| **Reasoned** | 思考・推論 | 内部でプランニング、Chain-of-Thought（思考の連鎖）、または自己批判を行った時。 |
| **Invoked** | ツール実行 | MCPツール、外部API、ローカルコマンド等、具体的な「道具」を使用した時。 |
| **Observed** | 環境観測 | ツールの実行結果、ログ、または外部の状態を読み取った時。 |
| **Refactored** | 修正・改善 | エラーやフィードバックに基づき、コードやアプローチを修正した時。 |
| **Resolved** | 完遂 | 与えられたミッションが成功裏に終了した時。 |
| **Abandoned** | 断念 | エラー、リトライ上限、または回復不能な事態によりタスクを中止した時。 |

## 2. データ構造の例 (JSON)

以下は、エージェントがコードの修正（Refactored）を試みたが、構文エラーが発生した際のxAPIステートメントの例です。

```json
{
  "actor": {
    "name": "Antigravity-Agent-01",
    "account": { 
      "homePage": "[https://github.com/antigravity](https://github.com/antigravity)", 
      "name": "agent-uuid-123" 
    }
  },
  "verb": {
    "id": "[https://w3id.org/xapi/chronicle/verbs/refactored](https://w3id.org/xapi/chronicle/verbs/refactored)",
    "display": { "ja-JP": "修正試行", "en-US": "refactored" }
  },
  "object": {
    "id": "[https://w3id.org/xapi/chronicle/activities/code-optimization](https://w3id.org/xapi/chronicle/activities/code-optimization)",
    "definition": {
      "name": { "ja-JP": "コードの最適化", "en-US": "Code Optimization" }
    }
  },
  "result": {
    "success": false,
    "extensions": {
      "[https://w3id.org/xapi/chronicle/ext/error_log](https://w3id.org/xapi/chronicle/ext/error_log)": "SyntaxError: invalid syntax at line 45",
      "[https://w3id.org/xapi/chronicle/ext/attempt_count](https://w3id.org/xapi/chronicle/ext/attempt_count)": 3
    }
  },
  "context": {
    "platform": "MCP-Server-v1.2",
    "extensions": {
      "[https://w3id.org/xapi/chronicle/ext/model](https://w3id.org/xapi/chronicle/ext/model)": "claude-3-5-sonnet"
    }
  }
}
