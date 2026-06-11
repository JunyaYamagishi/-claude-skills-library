---
name: graphic-record
description: 臨床論文のグラフィックレコード（インフォグラフィック画像）を作成するスキル。「グラフィックレコードを作成」「グラフィックレコードが登録されていない」「インフォグラフィックを作って」「論文を1枚の画像にまとめて」「グラフィックレコードを作成して下さい」など、論文のビジュアルサマリー・図解化・画像化を求めるあらゆるリクエストで必ず使用すること。PubMed論文データの取得 → 仕様書に従ったHTML設計 → PNG画像への変換 の一連のワークフローを担う。単一論文・複数論文どちらでも対応。Notionデータベースの論文管理との連携時（グラフィックレコード未登録の論文の特定・作成）でも必ず使用すること。
---

# グラフィックレコード作成スキル

臨床論文のグラフィックレコード（インフォグラフィック）を、定められた仕様書に従って作成するスキルです。

---

## ⚠️ 最重要：仕様書の参照

**このスキルを使う際は必ず最初に仕様書を読むこと。**

```
/mnt/skills/user/graphic-record/references/infographic_spec.yaml
```

仕様書には以下が定義されています：
- レイアウト（16:9 横長、上部ヘッダー + 3カラム）
- カラーパレット（グレー調ベース + アクセントブルー #2563EB）
- 各カラムの構成（左: SETTING / 中央: KEY RESULTS / 右: DISCUSSION・LIMITATION・CONCLUSION）
- デザインルール（アイコンは左カラムのみ、セクション見出しは英語、本文は日本語）

---

## ワークフロー

### Step 1: 論文情報の取得

**ユーザーがPMIDを提示している場合：**
```
pubmed:search_pubmed(query="XXXXXXXX[pmid]", output_mode="full")
```

**複数論文の場合は `OR` で一括取得：**
```
pubmed:search_pubmed(query="PMID1[pmid] OR PMID2[pmid] OR PMID3[pmid]", output_mode="full", maxResults=10)
```

**Notionデータベースから論文情報を引き継ぐ場合：**
すでに取得済みの `要約`・`著者`・`ジャーナル`・`発行年` プロパティをPubMedデータと組み合わせて使用する。

---

### Step 2: 仕様書を読む

```python
# 仕様書ファイルを参照
view("/mnt/skills/user/graphic-record/references/infographic_spec.yaml")
```

---

### Step 3: HTMLインフォグラフィックの作成

#### ファイル命名規則
```
/home/claude/graphic_record_{PMID}.html
```

#### HTMLの基本構造

```html
<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<style>
/* --- 基本リセットと body --- */
*{margin:0;padding:0;box-sizing:border-box}
body{
  width:1280px; height:720px;
  font-family:'Helvetica Neue',Arial,'Hiragino Kaku Gothic ProN','Noto Sans JP',sans-serif;
  background:#F3F4F6;
  display:flex; flex-direction:column;
  overflow:hidden
}

/* --- ヘッダー (#374151) --- */
.header{
  background:#374151; color:#fff;
  padding:18px 28px 14px;
  display:flex; flex-direction:column; justify-content:center;
  border-bottom:3px solid #4B5563;
  min-height:110px
}
.jp-title{font-size:18px; font-weight:800; line-height:1.4; margin-bottom:6px}
.en-subtitle{font-size:9.5px; color:#D1D5DB; line-height:1.5}
.pmid-badge{
  display:inline-block; background:#2563EB; color:#fff;
  font-size:8px; font-weight:700; padding:2px 7px; border-radius:3px;
  margin-left:8px; vertical-align:middle
}

/* --- 3カラムレイアウト --- */
.main{display:flex; flex:1; min-height:0}
.col-left  {width:30%; background:#F9FAFB; padding:14px 16px; border-right:1px solid #E5E7EB; overflow:hidden}
.col-center{width:40%; background:#FFFFFF;  padding:14px 16px; border-right:1px solid #E5E7EB; overflow:hidden}
.col-right {width:30%; background:#F3F4F6; padding:14px 16px; overflow:hidden}

/* --- セクション見出し --- */
.col-heading{
  font-size:9px; font-weight:800; letter-spacing:0.12em; color:#6B7280;
  margin-bottom:10px; border-bottom:2.5px solid #2563EB; padding-bottom:4px;
  text-transform:uppercase
}

/* --- 左カラム: アイコン付き項目 --- */
.item{display:flex; align-items:flex-start; margin-bottom:9px; gap:8px}
.icon-wrap{
  width:26px; height:26px; flex-shrink:0;
  display:flex; align-items:center; justify-content:center;
  border-radius:6px; margin-top:1px
}
.item-inner{flex:1}
.item-label{font-size:8px; font-weight:700; color:#2563EB; letter-spacing:0.06em; text-transform:uppercase; margin-bottom:2px}
.item-text {font-size:10.5px; color:#111827; line-height:1.55}

/* --- 右カラム: ブロック --- */
.right-block{margin-bottom:11px}
.right-label{
  font-size:8.5px; font-weight:800; color:#6B7280; letter-spacing:0.1em;
  margin-bottom:5px; border-left:3px solid #2563EB; padding-left:7px;
  text-transform:uppercase
}
.right-text{font-size:10.5px; color:#374151; line-height:1.6}
</style>
</head>
<body>

<!-- ヘッダー -->
<div class="header">
  <div class="jp-title">{日本語タイトル（結論を含む一文）}<span class="pmid-badge">PMID {PMID}</span></div>
  <div class="en-subtitle">{英語原題}.&nbsp;&nbsp;{著者}.&nbsp;&nbsp;{ジャーナル}. {年}. doi: {DOI}</div>
</div>

<div class="main">

  <!-- 左カラム: SETTING -->
  <div class="col-left">
    <div class="col-heading">SETTING</div>
    <!-- 各項目はアイコン + ラベル + テキストで構成 -->
    <!-- Study Design / Population / Exclusion / Data Source / Primary Outcome / Secondary Outcomes / Statistics -->
  </div>

  <!-- 中央カラム: KEY RESULTS -->
  <div class="col-center">
    <div class="col-heading">KEY RESULTS</div>
    <!-- SVGインライングラフ・表・フロー図を主役として配置 -->
    <!-- 文字はポイントのみ補足的に -->
  </div>

  <!-- 右カラム: DISCUSSION / LIMITATION / CONCLUSION -->
  <div class="col-right">
    <div class="col-heading">DISCUSSION / LIMITATION / CONCLUSION</div>
    <div class="right-block">
      <div class="right-label">DISCUSSION</div>
      <div class="right-text">{日本語で1〜3文}</div>
    </div>
    <div class="right-block">
      <div class="right-label">LIMITATION</div>
      <div class="right-text">{箇条書きで制約を列挙}</div>
    </div>
    <div class="right-block">
      <div class="right-label">CONCLUSION</div>
      <div class="right-text">{日本語で1〜3文}</div>
    </div>
    <!-- 最下部に CLINICAL TAKE-HOME ボックスを追加推奨 -->
  </div>

</div>
</body>
</html>
```

#### 左カラム アイコンの実装例（SVGインライン）

```html
<!-- Study Design アイコン（青） -->
<div class="icon-wrap" style="background:#EFF6FF">
  <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="#2563EB" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
    <rect x="3" y="4" width="18" height="18" rx="2"/>
    <line x1="16" y1="2" x2="16" y2="6"/>
    <line x1="8" y1="2" x2="8" y2="6"/>
    <line x1="3" y1="10" x2="21" y2="10"/>
  </svg>
</div>

<!-- Population アイコン（緑） -->
<div class="icon-wrap" style="background:#F0FDF4">
  <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="#16A34A" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
    <path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"/>
    <circle cx="9" cy="7" r="4"/>
    <path d="M23 21v-2a4 4 0 0 0-3-3.87"/>
    <path d="M16 3.13a4 4 0 0 1 0 7.75"/>
  </svg>
</div>

<!-- Exclusion アイコン（オレンジ） -->
<div class="icon-wrap" style="background:#FFF7ED">
  <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="#EA580C" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
    <circle cx="12" cy="12" r="10"/>
    <line x1="4.93" y1="4.93" x2="19.07" y2="19.07"/>
  </svg>
</div>

<!-- Primary Outcome アイコン（赤） -->
<div class="icon-wrap" style="background:#FFF1F2">
  <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="#E11D48" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
    <polyline points="22 12 18 12 15 21 9 3 6 12 2 12"/>
  </svg>
</div>

<!-- Statistics アイコン（緑） -->
<div class="icon-wrap" style="background:#ECFDF5">
  <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="#059669" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
    <line x1="18" y1="20" x2="18" y2="10"/>
    <line x1="12" y1="20" x2="12" y2="4"/>
    <line x1="6" y1="20" x2="6" y2="14"/>
  </svg>
</div>
```

#### 中央カラム: グラフ・図の種類と用途

| 論文タイプ | 推奨ビジュアル |
|-----------|--------------|
| RCT / 介入研究 | 前後比較棒グラフ（群別に色分け）|
| コホート研究 | ハザード比フォレストプロット風グラフ |
| 相関・妥当性研究 | 相関係数テーブル + バー |
| ガイドライン | 推奨クラス・エビデンスレベル表 |
| デバイス・センサー研究 | 性能指標テーブル + 感度バー |
| プロトコル論文 | 研究デザインフロー図 |

すべてインラインSVGで実装（外部ライブラリ不要）。

#### CLINICAL TAKE-HOME ボックス（右カラム下部に必ず追加）

```html
<div style="background:#F0FDF4;border-radius:6px;padding:8px 10px;margin-top:8px;border:1px solid #BBF7D0">
  <div style="font-size:8.5px;font-weight:800;color:#166534;letter-spacing:0.08em;margin-bottom:4px">📌 CLINICAL TAKE-HOME</div>
  <div style="font-size:10px;color:#15803D;line-height:1.6">{実臨床での簡潔なメッセージ}</div>
</div>
```

---

### Step 4: PNG変換

```bash
wkhtmltoimage \
  --width 1280 \
  --height 720 \
  --disable-smart-width \
  --zoom 1.0 \
  --format png \
  --encoding UTF-8 \
  /home/claude/graphic_record_{PMID}.html \
  /mnt/user-data/outputs/graphic_record_{PMID}.png
```

#### 複数論文の一括変換（bashループ）

```bash
for pmid in PMID1 PMID2 PMID3; do
  wkhtmltoimage --width 1280 --height 720 --disable-smart-width \
    --zoom 1.0 --format png --encoding UTF-8 \
    "/home/claude/graphic_record_${pmid}.html" \
    "/mnt/user-data/outputs/graphic_record_${pmid}.png" 2>&1 | tail -2
  echo "✅ ${pmid} done"
done
```

---

### Step 5: ファイルの提示

`present_files` ツールで全PNGを一括提示する：

```python
present_files([
  "/mnt/user-data/outputs/graphic_record_PMID1.png",
  "/mnt/user-data/outputs/graphic_record_PMID2.png",
  ...
])
```

---

## デザインチェックリスト

作成前に以下を確認すること：

- [ ] ヘッダー背景は `#374151`、文字は白
- [ ] 日本語タイトルにPMIDバッジ（青 `#2563EB`）を付記
- [ ] 左カラム: 全項目にSVGアイコン（色はアイコン種別で統一）
- [ ] 中央カラム: SVGグラフ/図が主役、テキストは補足のみ
- [ ] 右カラム: DISCUSSION / LIMITATION / CONCLUSION の3ブロック + TAKE-HOMEボックス
- [ ] セクション見出しはすべて英語大文字
- [ ] 本文はすべて日本語
- [ ] 画像サイズは 1280×720px（16:9）

---

## Notionとの連携時の補足

Notionの論文管理DBでグラフィックレコード未登録論文を特定する際のフロー：

1. `notion-fetch` でデータベーススキーマを確認
2. `notion-search` でデータソース内の全論文を検索
3. 各ページを `notion-fetch` し、`グラフィックレコード` プロパティが `[]`（空配列）であるものを抽出
4. 抽出されたPMIDのリストを作成し、上記ワークフローでグラフィックレコードを一括作成
5. 作成したPNGをユーザーに提示し、Notionへのアップロードを案内する

---

## 品質基準

- **文字サイズ**: 8px以上（wkhtmltoimage で 150DPI 相当）
- **グラフ**: 数値が正確で、X/Y軸ラベルが明記されていること
- **日本語タイトル**: 「結論を含む一文」として完結していること
- **PMID参照形式**: ユーザー設定に従い `{PMID}` 形式で記載
