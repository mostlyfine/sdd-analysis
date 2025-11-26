# 目的
Spec Driven Developmentを補助する各種ツールをアーキテクチャと設計思想の観点から比較・分析調査する。

# 対象ツール
- https://github.com/github/spec-kit
- https://github.com/bmad-code-org/BMAD-METHOD
- https://github.com/Fission-AI/OpenSpec
- https://github.com/snarktank/ai-dev-tasks
- https://github.com/ag2ai/ag2
- https://github.com/Pimzino/spec-workflow-mcp
- https://github.com/gotalab/cc-sdd
- https://github.com/classmethod/tsumiki
- https://github.com/jasonkneen/kiro
- https://github.com/Priivacy-ai/spec-kitty
- https://github.com/specpulse/specpulse
- https://github.com/nahisaho/musubi

# ルール
- 調査・分析結果は省略せず、十分に詳細に記載すること。
- リポジトリをローカル（`./sdd_tools`）にcheckoutし、分析時点の最新コードを対象として調査する。
- 各ツールについて以下を確認する：
  - READMEとドキュメント全体の精読
  - 主要なソースコード（特にコアロジック）の理解（全体のアーキテクチャ理解レベル）
  - IssueやPRから開発の方向性や課題を把握（Web検索）
  - 公式ドキュメントがあれば参照（Web検索）
- 必要に応じて外部情報の検索も行う（公式ドキュメント、解説記事など）。
- 情報が見つからない比較観点については、無理に推測せず「情報不明」または「該当する公開情報なし」と明記すること。

# 解説記事
- https://marmelab.com/blog/2025/11/12/spec-driven-development-waterfall-strikes-back.html
- https://medium.com/@visrow/github-spec-kit-vs-bmad-method-a-comprehensive-comparison-part-1-996956a9c653
- https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html

# 実行戦略（コンテキスト枯渇対策）

## フェーズ分割実行
各ツールを個別に分析し、中間成果物として保存することでコンテキストを効率管理する。

1. **フェーズ1**: 各ツール個別分析（1ツールずつ実行）
   - `analysis/{tool-name}.md` に出力
     - 例：
       - kiro → `analysis/kiro.md`
       - cc-sdd → `analysis/cc-sdd.md`
       - spec-kit → `analysis/spec-kit.md`

2. **フェーズ2**: 統合レポート作成
   - 全ツールの個別分析を統合
   - 出力: `analysis-report.md`

## 各フェーズ実行ルール
- 1フェーズ完了後、次フェーズ実行前にユーザー確認を取る
- 個別分析は Task tool (subagent_type=Explore, thoroughness="very thorough") を活用推奨
- 中間ファイルは必ず保存し、データ損失を防ぐ

## 分析深度レベル
各ツールは以下のレベルで分析を実施：

- **Level 1（基礎調査）**: README + package.json/設定ファイル + ディレクトリ構造
- **Level 2（標準調査）**: Level 1 + コアロジック解析 + 主要ドキュメント
- **Level 3（詳細調査）**: Level 2 + 全ドキュメント + Issue/PR分析 + 外部情報検索

基本は Level 2 で実施し、必要に応じて Level 3 へ深掘りする。

# 比較観点

## 【必須】全ツール必須調査項目
以下は全ツールで必ず詳細調査すること：
- 基本コンセプト（ツールとしての思想、目的）
- 核心技術
- ワークフロー
- 技術スタック
- プロジェクト構造
- 提供機能・ツール
  - コア機能（基本的な仕様駆動開発機能）
  - 差別化機能（独自の特徴的な機能、向き不向き）

## 【重要】可能な限り調査
情報が入手可能であれば詳細調査すること：
- 統制メカニズム（仕様（Spec）の変更、レビュー、承認に関するワークフローや仕組み）
- プロジェクト記憶（仕様の変更履歴や、その背景にある議論・決定をどのように記録・管理・参照するか）
- エコシステム
- ポータビリティ
- 導入アプローチ（チーム規模、状況などを考慮）
- 既存プロジェクトに対する分析能力
- 言語対応

## 【補足】情報があれば追加
追加情報として調査（情報不足の場合は明記して省略可）：
- SWOT分析
- 実践的な選定基準
- ユースケース
- 課題、制約、注意点

# Output Format および出力ボリューム

## 個別分析ファイル（`analysis/{tool-name}.md`）

- GitHub Flavored Markdown（.md）で出力する。
- セクション順・項目順は固定。また各項目は必要な場合のみ記載。
- フロントマターはYAMLで記述。
- 出力は各項目ごとに明確かつ簡潔にまとめること。
- 1項目あたり原則2～4文・段落以内で抑える。

```markdown
---
tool_name: Kiro
repository_url: https://github.com/jasonkneen/kiro
analyzed_at: 2024-06-15
analysis_level: 2
ai_model_used: GPT-4o
commit_hash: 8a2b1c3
---

# ツール概要
Kiroは…（1-2段落の要約）

# 比較観点ごとの分析結果

## 基本コンセプト
- 概要: …（要点を2-3段落で）
- 調査・分析結果: …（マトリクス、箇条書き、mermaid なども可）
- 考察: …（解釈・意見）
- データソース: …（ファイルパス、URL、コミットハッシュなど）

## 核心技術
…（他の項目と同様にまとめる）

## ワークフロー
…
（以下、各必須項目・重要項目・補足項目を同順で記述。情報不明であれば「情報不明」と明記。）

# エラー・情報不明項目
- 日付などの必須フィールド欠落時は「N/A」と記載。
- 情報不明の比較観点は「情報不明」または「該当する公開情報なし」と出力。
```

## 統合レポートファイル（`analysis-report.md`）

- GitHub Flavored Markdown（.md）で出力。
- セクション順・項目順は固定。
- フロントマターはYAMLで記述。
- 各セクション・分析項目とも2～4文・段落以内に抑える。
- 比較表・箇条書きも可。ただし6項目以内・1行で収める。

```markdown
---
title: SDD分析レポート（2024-06-15）
analyzed_at: 2024-06-15
target_tools:
  - https://github.com/jasonkneen/kiro
  - ... # 省略
ai_agent_used: GPT-4o
ai_model_used: GPT-4o
---

# エグゼクティブ・サマリ
全体概要（1-2段落程度）

## 比較観点ごとの分析結果（PREP法ベース）

### 基本コンセプト
- サマリ: …（2-3文）
- 調査・分析結果: …（表形式、全ツール横断比較。各ツール名列を含む）
- 結果の解釈・考察
- データソース（analysis/{tool-name}.md への参照など）

### 核心技術
…（個別分析時と同順で各必須項目・重要項目・補足項目を記述）

## 総合比較表
- 全ツールの主要特徴を表形式で一括記載。
- カラム順：ツール名／基本コンセプト／核心技術／ワークフロー／技術スタック（以下、必須項目順）。

## 結論

# エラー・情報不明項目
- 「情報不明」「該当する公開情報なし」「N/A」を明記。
- 必須フィールド欠落時はN/A。
```

#### その他の出力／記述ガイドライン
- 各項目は、必須でなければ省略可。
- 表現は厳密なテンプレートでなくとも、同種項目は同順・同タイトルで記述すること。
- markdown内で表・箇条書き・mermaid diagram・マトリクスなど多様な構造化手法を使ってよい。
- エラーや必須情報不明の場合は、適切に「N/A」「情報不明」等を明示すること。
- analysis_level（分析深度）に応じて省略可能部分は省略可。必須項目は漏れなく記載すること。

## 出力ボリューム指示（Output Verbosity）
- すべての応答・レポート・表・段落・各項目について、2段落または6項目以内に収めること。
- 各段落・箇条書きは短く簡潔に。必要以上の説明は避けてください。
- 比較表や箇条書きは最大6行・1文ずつに制限します。
- 丁寧さや配慮のために記述を冗長にしないでください（Do not increase length to restate politeness）。
- ユーザーアップデートや説明は1～2文。ユーザーから明示的な要望があるときのみ長文を許可します。

## 回答品質について
- 完全性とアクション可能な回答を優先し、極端に要約しすぎないこと。ただし、すべて所定の字数・段落・項目数内に収めてください。
- ユーザー入力が短文でも、必要な調査・分析と、情報網羅を優先してください。
