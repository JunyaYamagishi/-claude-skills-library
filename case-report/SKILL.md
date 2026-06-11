---
name: case-report
description: "英文症例報告（Case Report）のインタラクティブ執筆支援。ユーザーと対話しながら、Why This Case? → Author Guideline確認 → 症例情報収集 → 不足情報質問 → 原稿生成 → 文献引用 → Word数調整の順で進行する。「症例報告を書きたい」「case reportを書く」「Case Reportを英語で」「症例をまとめたい」「ケースレポート執筆」「case report draft」「症例報告の原稿作成」「clinical case write up」「BMJ Case Reports投稿」「症例報告のテンプレート」「case report template」などの要求で必ず使用する。症例報告に関連する英語化・執筆・テンプレート提供のすべてに適用する。"
---

# Case Report Writing Skill

英文症例報告（Case Report）をユーザーと対話式に起草する。CARE reporting guidelineに準拠し、投稿先のAuthor Guidelineに合わせた原稿を生成する。

## 対話フロー（この順序を厳守し、飛ばさない）

```
Phase 1: Why This Case?（症例の意義を明確化）
  ↓
Phase 2: Author Guideline入力（投稿先の規定を確認）
  ↓
Phase 3: 症例情報入力（ファイルまたは会話で収集）
  ↓
Phase 4: 不足情報質問（テンプレート照合で欠損を特定）
  ↓
Phase 5: 原稿生成（セクション別にドラフト）
  ↓
Phase 6: 文献引用付与（PubMed検索で根拠を補強）
  ↓
Phase 7: Word数調整・CARE checklist確認
```

---

## Global Rules（全フェーズ共通）

1. **対話言語**: ユーザーとのやり取りは日本語。原稿本文は英語
2. **捏造禁止**: 数値・PMID・DOI・検査結果を絶対に捏造しない。不明点は `[TBD: ○○]` とマークする
3. **匿名化**: 患者情報は匿名化を促す。氏名・具体的住所・ID・特定性の高い日付は削除/相対化する提案をする（例: 年齢→年代、日付→入院X日目）
4. **段落中心**: 本文に箇条書きを使わず、段落で論理展開する
5. **太字禁止**: 原稿本文に **Bold** フォントを使用しない
6. **時制**: 患者固有の出来事は過去形、一般的事実は現在形
7. **文体**: 簡潔・客観的・フォーマルな学術英語。冗長表現を排除する
8. **Hedging**: 不確実な主張には may, could, suggests などを適切に使用する
9. **Writing Rules**: `references/writing-rules.md` を読み込み、全ドラフトに適用する

---

## Phase 1: Why This Case?

**会話開始時に必ずこの3つを質問する:**

```
症例報告の執筆を始めましょう。まず以下の3点を教えてください:

1. この症例の新規性・稀少性は何ですか？
2. 既存の知見と異なる点（意外性・診断/治療上のギャップ）は何ですか？
3. 読者へのLearning Pointを3つ以内で書くと？

短文・箇条書きでOKです。
```

ユーザーの回答が曖昧な場合は、具体化するために追加質問する。この3点は論文のIntroductionとDiscussionの骨格になるため、ここで明確にしておくことが重要。

---

## Phase 2: Author Guideline確認

Why This Case? が埋まったら以下を依頼する:

```
次に、投稿先ジャーナルのAuthor Guidelineを教えてください。
URLでも本文コピペでも構いません。

可能であれば以下もお知らせください:
- 原稿種別（Case Report / Clinical Image / Letter 等）
- Word limit（Abstract / 本文）
- 図表数上限
- References形式（Vancouver等）
```

**Guideline受領後に内部メモとして以下を構造化して保持する:**

- セクション構成（必須見出し、順序、Abstract構造化の要否）
- Word limit（Abstract / 本文 / 各章の目安）
- 図表上限、図表キャプション規則
- 引用スタイル（番号順、著者数、雑誌略名など）
- 倫理: 同意取得の書き方、IRB記載要否
- CARE guideline提出要否
- 英語/日本語指定、スペリング（US/UK）

**ユーザーがGuidelineを持っていない場合**: BMJ Case Reportsのガイドラインに従う。web_searchで「BMJ Case Reports author guidelines template」を検索し、テンプレートPDFやInstructions for Authorsページを取得して確認する。BMJ Case Reportsの主要ルール: セクション構成は Summary(150語以内) → Background → Case Presentation → Investigations → Differential Diagnosis → Treatment → Outcome and Follow-up → Discussion → Learning Points(3-5個) → Patient's Perspective。著者数上限4名、引用はVancouverスタイル、患者同意必須、Titleに "a case report" を含めない。

---

## Phase 3: 症例情報入力

```
症例情報が入ったファイルをアップロードしてください。
PPTのPDF、Word、抄録、スライド等どんな形式でもOKです。
複数ファイルでも構いません。

まだ情報をまとめていない場合は、テンプレートを提供しますので
それに沿って入力していただくこともできます。
```

**テンプレート提供判断**: ユーザーがファイルを持っていない、または「何を書けばいいかわからない」と言った場合、`assets/CaseReport_Template.md` を読み込んで提供する。提供時にはYAMLフロントマター（`---` で囲まれた先頭部分）を削除し、ユーザーが記入しやすい形に整える。テンプレートの全項目を埋める必要はないことを伝え、わかる範囲での入力を促す。

**ファイル受領後の処理**:
1. アップロードされた全ファイルの内容を読み取る
2. ファイル間の矛盾がないか確認する（矛盾があればユーザーに確認）
3. Phase 4へ進む

---

## Phase 4: 不足情報質問

`assets/CaseReport_Template.md` の構成に照らし合わせ、原稿執筆に必要だが未提供の情報を特定する。

**質問ルール**:
- 質問は1回あたり最大7個に制限する（多すぎるとユーザーの負担になる）
- 原稿に必須の情報を優先する（優先度: 主訴・現病歴・検査・治療・転帰 > 既往歴・家族歴 > 生活歴）
- 全項目が埋まっていなくても執筆に十分と判断すればスキップ可能
- 匿名化が必要な情報には具体的な置換提案を添える

**最低限確認すべき項目**:
- 年齢（年代で可）、性別
- 主訴、現病歴のタイムライン
- 主要検査結果（ラボ、画像、病理、培養）
- 鑑別診断と除外根拠（最低2-3個）
- 治療介入（薬剤名、用量、期間、処置）
- 転帰（退院、フォロー、再発、死亡など）
- 患者同意（取得済み / 予定 / 不要の理由）

---

## Phase 5: 原稿生成

### 事前準備（原稿作成前に必ず実行）

1. `references/writing-rules.md` を読み込む
2. `references/care-checklist-items.md` を読み込む
3. Phase 2で保持したAuthor Guideline内部メモを確認する

### セクション構成

Author Guidelineに指定がなければ以下の標準構成で執筆する:

```
Title
Abstract（構造化: Introduction / Case Presentation / Discussion / Conclusion）
Keywords
Introduction
Case Presentation
  - Patient Information
  - Clinical Findings
  - Timeline
  - Diagnostic Assessment
  - Therapeutic Intervention
  - Follow-up and Outcomes
Discussion
Conclusion
Patient Perspective（該当する場合）
Informed Consent Statement
References
```

### セクション別執筆ガイド

#### Title
- 診療領域とCase Reportであることが明確にわかるタイトル
- 簡潔で具体的に（目安: 15語以内）

#### Abstract
- Author Guidelineの構造に従う（構造化 or 非構造化）
- Word limitを厳守する
- 症例の新規性・学習点を明確にする

#### Introduction
- 背景知識を2-3段落で簡潔に記述する
- 本症例を報告する意義（Phase 1のWhy This Case?を反映）
- 関連する既報のCase Reportや文献を引用する
- PubMed検索で関連文献を取得する（Phase 6と並行）

#### Case Presentation
- 時系列に沿って記述する
- 陰性所見（pertinent negatives）も含める — 鑑別診断の除外に重要な所見
- 検査値はSI単位を基本とする（Guidelineの指定に従う）
- Timelineの表やFigureを提案する

#### Discussion
- 第1段落: 症例の要約（1段落、具体的数値は入れない）
- 第2-3段落: 文献レビュー。既報との類似点・相違点を議論する。PubMed検索が必須
- 第4段落: Limitations and Strengths
- 第5段落: Conclusion。Learning Pointsを明確にする（Phase 1を反映）

### 出力形式

各セクションの出力時に以下を含める:
- A. ドラフト本文（引用がある場合は{PMID}込み）
- B. セルフチェック結果（Writing Rulesに照らした確認）
- C. 提案（ブラッシュアップする / 次のセクションに進む / Timelineの図表提案など）

---

## Phase 6: 文献引用

### いつ検索するか
- 稀少性の主張（「X例目の報告」など）
- 既報との類似点・相違点の議論
- 治療選択の根拠
- 予後や合併症の頻度
- 一般的事実でも引用が慣例的に求められる箇所

### PubMed検索手順

1. 研究テーマからコア概念を抽出し、適切な MeSH term に変換する
2. MeSH termを組み合わせて検索式を作成する
3. `count` で検索式の結果数を確認し、適切な件数（目安: 20-200件）になるよう調整する
4. `search` でMeSH検索を実行する
5. 結果が不十分な場合は検索式を修正して再検索する
6. `fetch` または `fetch_batch` でAbstractを取得する
7. 症例報告・レビュー・ガイドライン・High Impact誌を優先して選定する

### 引用形式
- 本文中に `{PMID}` を埋め込む
- References節はAuthor Guidelineの指定に従う（指定なければVancouverスタイル）
- 各引用に 1st author, 雑誌名, 発刊年, PMIDへのハイパーリンクを記載する

### PubMedツールが使えない場合
その旨を明示し、検索クエリ候補と引用差し込み位置をマークした「引用なしドラフト」を提示する。

---

## Phase 7: Word数調整・CARE Checklist確認

### Word数調整
1. Author Guidelineのword limitと現在のword数を比較する
2. 超過している場合は具体的な削減提案をする（どのセクションから何語削減するか）
3. 不足している場合は補強すべき箇所を提案する

### CARE Checklist確認
`references/care-checklist-items.md` の全13項目に照らして原稿をチェックする。

チェック結果を以下の形式で提示する:

```
CARE Checklist 確認結果:

| # | Item | Status | Location / Comment |
|---|------|--------|--------------------|
| 1 | Title | ✅ | Title section |
| 2 | Keywords | ✅ | Keywords section |
| ...| ... | ✅/⚠️/❌ | ... |
```

- ✅ 充足
- ⚠️ 部分的に記載あり（改善提案を付記）
- ❌ 未記載（追記案を提案）

### 最終成果物

原稿が完成したら:
1. 完成原稿をMarkdownファイルとして保存する
2. CARE checklistの充足状況サマリーを添付する
3. Word countレポートを提示する
4. 必要に応じてdocx形式への変換を提案する

---

## SOP再読み込みルール

会話が長くなるとコンテキストが失われやすいため、以下のタイミングで参照ファイルを再読み込みする:

| タイミング | 読み込むファイル |
|---|---|
| Phase 5着手時 | `references/writing-rules.md`, `references/care-checklist-items.md` |
| Discussion執筆時 | `references/writing-rules.md`（再読み込み） |
| Phase 7着手時 | `references/care-checklist-items.md`（再読み込み） |

---

## 補助リソース

- **`references/writing-rules.md`** — Academic English Writing の13ルール + AI表現回避リスト
- **`references/care-checklist-items.md`** — CARE reporting checklist の全13項目
- **`assets/CaseReport_Template.md`** — 症例情報入力用テンプレート（ユーザーに提供可能）

## 関連スキル

- **`academic-write`** — 英文校正・推敲（write/revise/reviewモード）
- **`clinical-paper`** — 臨床研究論文のセクション別執筆支援
- **`peer-review`** — 査読コメントの英語化
