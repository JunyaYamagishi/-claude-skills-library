---
name: clinical-paper
description: "医学論文（臨床研究）のセクション別執筆支援。Methods, Results, Introduction, Discussionをインタラクティブに起草する。/clinical-paper で起動し、セクション選択→情報収集→ドラフト→レビューの流れで進行する。論文執筆、臨床研究論文、manuscript drafting に使用する。"
allowed-tools: Read, Write, Edit, Glob, Grep, Bash, Task, ToolSearch, AskUserQuestion, mcp__pubmed__search_pubmed, mcp__pubmed__get_full_abstract, mcp__pubmed__count_results, mcp__pubmed__find_similar_articles, mcp__pubmed__batch_process
---

# Clinical Paper Drafting Skill

医学論文（臨床研究）のセクション別インタラクティブ執筆支援を行う。ユーザーと対話しながら、情報収集→ドラフト作成→チェック→ブラッシュアップのサイクルを回す。

## 引数

```
$ARGUMENTS = [section] [file_path]
```

- **section**（任意）: `methods`, `results`, `introduction`, `discussion`
- **file_path**（任意）: 出力先のMarkdownファイル

引数が省略された場合はインタラクティブに確認する。

---

## 推奨執筆順序

**Methods → Results → Introduction → Discussion** の順を推奨する。理由:
1. Methods: 研究計画が最も客観的で書きやすい
2. Results: Methods確定後にデータを記述
3. Introduction: Results を踏まえてGapを明確化
4. Discussion: 全体を俯瞰して解釈・考察

ユーザーが別の順を希望する場合はそれに従う。

---

## Global Operating Rules（全セクション共通・厳守）

1. **質問優先**: ドラフト本文はユーザーから必要最小限の情報が揃うまで出力しない。情報不足時は最大5個の確認質問を日本語で提示する
2. **捏造禁止**: 不確実な点は「不明」「追加情報が必要」と明示。数値・PMID・DOIを捏造しない
3. **セクション境界の厳守**:
   - Results: 解釈・考察・因果推論を一切書かない
   - Methods: 結果語彙（significant等）を使わない
   - Introduction: 結果を先取りしない
   - Discussion: 新規データを追加しない
4. **段落中心**: 箇条書きを避け、段落で論理展開する
5. **対話言語**: ユーザーとのやり取りは日本語。ドラフト本文と引用は英語
6. **Academic Writing Rules**: `references/writing-rules.md` のルールを全ドラフトに適用する

### 出力形式（各セクション共通）
A. 不足情報の確認（ある場合のみ）
B. ドラフト本文（引用がある場合は {PMID} 番号込み）
C. チェック（ガイドライン観点・表記・図表提案）
D. 引用文献リスト（使用した場合）
E. 提案（ブラッシュアップするか、次のセクションに進むか）

---

## SOP再読み込みルール（重要）

**会話が長くなるとSOPの詳細が失われるため、各セクション着手時に必ずSOPファイルを再読み込みすること。**

前のセクションで同じファイルを読み込み済みでも、新しいセクションに着手する際は改めて読み込む。これは忘却防止のための必須手順である。

| セクション | 読み込むSOPファイル | 追加で読み込むファイル |
|---|---|---|
| Methods | `references/sop-methods.md` | `references/equator-checklists.md`, `references/writing-rules.md` |
| Results | `references/sop-results.md` | `references/writing-rules.md` |
| Introduction | `references/sop-introduction.md` | `references/writing-rules.md` |
| Discussion | `references/sop-discussion.md` | `references/writing-rules.md` |

---

## インタラクティブフロー

### Phase 1: セクション確定

`$ARGUMENTS` にセクション指定がある場合はそれに進む。ない場合:

```
どのセクションを執筆しますか？
推奨順序: Methods → Results → Introduction → Discussion

1. Methods（研究方法）
2. Results（結果）
3. Introduction（序論）
4. Discussion（考察）
```

### Phase 2: SOP読み込み + 情報収集

**セクション確定後、ドラフト作成前に必ず以下を実行する:**

1. **該当セクションのSOPファイルを Read で読み込む**（上記「SOP再読み込みルール」の表を参照）
2. **`references/writing-rules.md` を Read で読み込む**
3. SOPに従い情報収集を開始する

**共通ルール**:
- ユーザーがファイル（プロトコル、統計計画、解析表など）を持っている場合はアップロードを促す
- 質問は最大5個に制限する
- 不足情報は本文中に `[TBD: ○○]` としてマークし、後で補完可能にする

### Phase 3: ドラフト作成

**Phase 2で読み込んだSOPの構成と規律に厳密に従い**、英語でドラフトを作成する。

以下は各セクションの最重要ルール要約（SOPの詳細は必ずファイルから読み込むこと）:

#### Methods
> **SOP: `references/sop-methods.md`** — 着手前に必ず Read すること
> - Subheading: Study design / Participants / Intervention / Outcomes / Statistical analysis / Ethics
> - EQUATOR準拠チェック（`references/equator-checklists.md`）
> - 結果語彙（significant等）禁止。再現可能性を最優先

#### Results
> **SOP: `references/sop-results.md`** — 着手前に必ず Read すること
> - 解釈・考察を一切含めない
> - "suggest/indicate/consistent with/mechanism" 禁止
> - 構成: Study flow → Baseline → Primary → Secondary → Safety

#### Introduction
> **SOP: `references/sop-introduction.md`** — 着手前に必ず Read すること
> - 3段落構成を厳守: Known Facts → Gap → Purpose
> - PubMed検索必須（最大10本）
> - 目的段落は2-3文のみ。結果の先取り禁止

#### Discussion
> **SOP: `references/sop-discussion.md`** — 着手前に必ず Read すること
> - 原則5段落: Summary → Literature Review (2段落) → Limitations & Strengths → Conclusion
> - PubMed検索必須（20本程度）、第2-3段落に引用重点配分
> - Summary段落に具体的数値を入れない

### Phase 4: PubMed検索（Introduction・Discussion）

Introduction と Discussion では PubMed検索が必須。

**検索手順**:
1. 研究テーマからコア概念を抽出し、適切なMeSH termに変換する
2. `mcp__pubmed__count_results` で検索式の結果数を事前確認する
3. `mcp__pubmed__search_pubmed` でMeSHタグ付き検索を実行する（例: `"Neoplasms"[MeSH]`）
4. 結果が不十分な場合は検索式を再構築して再検索する
5. `mcp__pubmed__get_full_abstract` で候補文献のアブストラクトを取得する
6. 総説・ガイドライン・ランドマーク研究を優先して選定する

**引用形式**:
- 本文中に `{PMID}` を埋め込む
- ドラフト末尾にPMID付き引用文献リストを提示する

PubMedツールが利用できない場合: その旨を明示し、検索クエリ候補と引用差し込み位置をマークした「引用なしドラフト」を提示する。

### Phase 5: レビューと次のステップ

ドラフト完成後、以下を提示する:
1. **セルフチェック結果**: Academic Writing Rules（`references/writing-rules.md`）の13ルールに照らした自己チェック
2. **EQUATORチェック**（Methods時）: 不足項目のサマリー
3. **図表提案**: 推奨するTable/Figure構成
4. **次のアクション提案**:
   - このセクションをブラッシュアップする
   - 次のセクションに進む（推奨順序に基づき提案）
   - ファイルに保存する

**次のセクションに進む場合:**
次のセクション着手時に Phase 2 に戻り、該当SOPファイルと writing-rules.md を改めて Read で読み込むこと。既に読み込み済みであっても必ず再読み込みする（忘却防止）。

---

## 補助リソース

### セクション別SOP（セクション着手時に該当ファイルを読み込む）
- **`references/sop-methods.md`** — Methods セクション詳細SOP
- **`references/sop-results.md`** — Results セクション詳細SOP
- **`references/sop-introduction.md`** — Introduction セクション詳細SOP
- **`references/sop-discussion.md`** — Discussion セクション詳細SOP

### 全セクション共通
- **`references/section-sops.md`** ([[50_coding/Claude_plugin_doc/clinical-paper-plugin/skills/clinical-paper/references/section-sops]]) — 全セクションの統合SOP（通読用）
- **`references/equator-checklists.md`** ([[50_coding/Claude_plugin_doc/clinical-paper-plugin/skills/clinical-paper/references/equator-checklists]]) — CONSORT/STROBE/PRISMA/STARD/CARE の必須項目チェックリスト
- **`references/writing-rules.md`** ([[50_coding/Claude_plugin_doc/clinical-paper-plugin/skills/clinical-paper/references/writing-rules]]) — Academic English Writing の13ルール + AI表現回避リスト

## 関連スキル

- **`academic-write`** ([[.claude/skills/academic-write/SKILL]]) — 英文校正・推敲（write/revise/reviewモード）
- **`ref-verify`** ([[.claude/skills/ref-verify/SKILL]]) — 引用と参考文献の整合性検証
- **`note-write`** ([[.claude/skills/note-write/SKILL]]) — note.com向け技術記事執筆
