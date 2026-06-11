---
tags:
  - medical-manuscript
  - academic-writing
  - clinical-research
  - workflow
  - writing
  - equator-network
---

# Section SOPs — 各セクション詳細手順（統合版）

> **Note**: このファイルは全セクションの統合参照用です。
> 実際の執筆時は、各セクション着手時に該当する個別SOPファイルを読み込んでください:
> - `sop-methods.md` / `sop-results.md` / `sop-introduction.md` / `sop-discussion.md`

## Methods SOP

### ゴール
研究の再現可能性を担保するMethods草案を、主要Subheadingで整理して作成する。

### 1) 研究デザインの確認
まずデザインを確定する: RCT / cohort / case-control / cross-sectional / diagnostic accuracy / case report / systematic review

### 2) 情報収集（ファイル優先）
- 研究プロトコル、統計解析計画書、IRB承認、登録情報、データ定義書、解析出力（Table 1の元データ等）があればアップロードを促す
- ファイルがない場合は必須項目を質問（最大5問）し、不足は `[TBD]` として本文にマークする

### 3) EQUATOR準拠チェック
- 研究デザインに応じて `equator-checklists.md` ([[50_coding/Claude_plugin_doc/clinical-paper-plugin/skills/clinical-paper/references/equator-checklists]]) を参照し、必須項目の不足を洗い出す
- 不足が致命的な場合は先に質問してからドラフトを書く

### 4) 最低限必要なSubheading
1. Study design and setting
2. Participants (eligibility criteria)
3. Intervention/Exposure (and comparator) or Index test/Reference standard
4. Outcomes (definitions)
5. Statistical analysis
6. Ethics approval and consent

必要に応じて追加:
- Sample size calculation
- Handling of missing data
- Sensitivity / subgroup analyses

### 書き方の規律
- 結果語彙（significant等）を使わない。Methodsは計画と手順のみ
- 解析は "what and how" を明確に（モデル名、共変量、閾値、両側/片側、有意水準）
- 測定・評価者・ブラインド化・再現性（interobserver等）があれば記載

### ドラフト完成時の出力
- EQUATOR観点の不足項目（短い箇条書き、必要時のみ）
- 追加で推奨する付録・図表（フローチャート等）

---

## Results SOP

### ゴール
解釈を含めず、得られた結果を淡々と記述するResults草案を作成する。

### 入力（ユーザーに求める最小情報）
- 対象背景（Demographics; Table 1相当）: N、年齢、性別、主要共変量、群別比較
- 主要アウトカム（Main Results）: 群別/時点別の数値、効果量、CI、P値
- 追跡期間、欠測、除外、解析対象（ITT/PP等）

不足があれば質問は最大5個まで。

### ルール（最重要）
- **解釈・考察を一切含めない**
- "suggest/indicate/consistent with/associated with（因果含意）/mechanism/clinically meaningful" 等の語彙を禁止
- 数値の羅列を避け、Table/Figure参照の文を入れる

### 推奨構成
1. Study flow / analyzed population（Figure 1参照を推奨）
2. Baseline characteristics（Table 1参照）
3. Primary outcome（Table 2 / Figure 2参照）
4. Secondary outcomes / subgroup / sensitivity（必要時）
5. Adverse events / safety（該当時）

### ドラフト完成時の出力
- 推奨する図表構成案（Table 1, Figure 1...）

---

## Introduction SOP

### ゴール
3段落（合計A4 1ページ程度）のIntroduction草案を作成する。

### 入力（ユーザーに求める最小情報）
- 対象領域/疾患
- 介入/曝露（または検査・手技）
- 比較対象（ある場合）
- 主要アウトカム（1つでよい）
- 研究デザイン（ざっくりでよい: e.g., retrospective cohort）

不足があれば質問は最大5個に制限。

### 構成（3段落構成を厳守）

#### 第1段落: Known Facts (Background)
- その分野の一般的背景と既知の事実
- 読者が研究課題を理解するための最小限に絞る（総説のように広げない）

#### 第2段落: Unknown Facts / Gap
- 現時点で未解明、議論が分かれる点、エビデンスの不足を明確化
- 可能なら相反する知見を1組以上提示する

#### 第3段落: Purpose / Hypothesis
- 研究目的を**1-2文**で明確・簡潔に述べるのみ（厳守）

### PubMed検索（必須、最大10本程度）
- 総説/ガイドライン/主要コホート/ランドマークを優先
- Background → Gap → Purpose に適切に分配

### ドラフト完成時の出力
- "このIntroductionで主張しているGap" を1文で明示
- 引用文献リスト（PMID付き）

### 失敗パターン回避
- 目的段落が長くなる → 2-3文に切る
- 結果の先取り（"We found…"等） → 禁止
- 研究背景を広げ過ぎる → 研究課題に直結する情報のみ

---

## Discussion SOP

### ゴール
原則5段落のDiscussion草案を作成し、PubMed文献を引用しながら論理的に議論を展開する。

### 事前確認（最小情報）
- Discussionで強調したい論点（主張）
- 主要結果の要旨
- 研究デザイン、対象、主要アウトカム

不足があれば質問は最大5個まで。

### 構成（原則5段落）

#### 第1段落: Summary
- 主要結果を1-2文で要約（**具体的数値は提示しない**）
- 新規のデータは入れない

#### 第2-3段落: Literature Review & Interpretation
- 各段落は **Topic sentence → Supporting sentences（根拠と引用） → 必要に応じてConcluding sentence（橋渡し）** を厳守
- 過去知見との比較・一致/不一致の理由、なぜ今回のような結果になったかに関する考察を述べる
- 過剰な推測は避け、推測は "may / might" 等で明示
- それぞれの段落で十分な数の文献を引用して議論を展開する
- 分量は短いものよりは必要十分な長さが好まれる

#### 第4段落: Limitation & Strength
- 限界と強みを記述
- ユーザー入力がない場合はデザインと結果から論理的に想定される限界案を提示し「確認が必要」と明示

#### 第5段落: Conclusion
- 3文程度。第1段落の言い換えではなく、臨床的・科学的意義を含めて結ぶ
- 過度な一般化や因果断定を避ける

### PubMed検索（必須、20本程度）
- 第2-3段落に重点配分
- Summary/Conclusionは引用しない

### ドラフト完成時の出力
- 引用文献リスト（PMID付き）
