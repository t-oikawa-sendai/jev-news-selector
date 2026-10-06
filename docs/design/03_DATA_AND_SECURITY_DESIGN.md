# Data and Security Design（データ・セキュリティ設計）

<!-- Document Info（文書情報） -->
| Item（項目） | Value（値） |
|---|---|
| Document ID（文書ID） | DATA-001 |
| Version（バージョン） | 0.1 |
| Status（ステータス） | Draft |
| Created Date（作成日） | 2026-10-06 |
| Last Updated（最終更新日） | 2026-10-06 |
| Owner（管理者） | Takashi Oikawa |
| Related Documents（関連文書） | README.md / 02_REQUIREMENTS_DEFINITION.md / 04_UI_AND_FLOW_DESIGN.md / 05_ARCHITECTURE_DESIGN.md |

---

## Table of Contents（目次）

1. [Purpose（目的）](#1-purpose目的)
2. [Scope（対象範囲）](#2-scope対象範囲)
3. [Out of Scope（対象外範囲）](#3-out-of-scope対象外範囲)
4. [Assumptions（前提条件）](#4-assumptions前提条件)
5. [Definition Details（定義内容）](#5-definition-details定義内容)
6. [Open Issues（未決事項）](#6-open-issues未決事項)
7. [Handoff to Detail Design（詳細設計への引き継ぎ）](#7-handoff-to-detail-design詳細設計への引き継ぎ)

---

## 1. Purpose（目的）

本文書は、`jev-news-selector` のデータ・保存・セキュリティの正本である。Obsidianへ保存するMarkdownの配置・命名・YAML frontmatter・本文構成・URL一意性・再処理時の更新規則と、秘密情報の取り扱いを定義する。

読者は、設計担当・実装担当である。

---

## 2. Scope（対象範囲）

- Obsidian Vault 内の保存先フォルダ構成
- 記事Markdownのファイル単位・ファイル名規則
- 最終記事URLによる一意性
- 記事Markdownの YAML frontmatter と本文の構成
- 再処理時の更新項目と保持項目
- 秘密情報と保存データのセキュリティ方針

---

## 3. Out of Scope（対象外範囲）

- データベース。本Botはデータベースを使用しない
- 人間評価の入力操作。O-03（[04_UI_AND_FLOW_DESIGN.md](./04_UI_AND_FLOW_DESIGN.md)）で管理する
- 既存Markdownの検索方式と最終記事URLの正規化方式。O-04（[05_ARCHITECTURE_DESIGN.md](./05_ARCHITECTURE_DESIGN.md)）で管理する
- 自動選別条件。未決であり、本文書で定めない

---

## 4. Assumptions（前提条件）

- Obsidian Vault は利用者のMac上に存在し、Git Repository の外に置く
- 処理日・公開日は Asia/Tokyo（JST）の日付として扱う（公開日の規則は [02_REQUIREMENTS_DEFINITION.md](./02_REQUIREMENTS_DEFINITION.md) §5.1.4）
- 最終記事URLをシステム上の一意キーとする（[02_REQUIREMENTS_DEFINITION.md](./02_REQUIREMENTS_DEFINITION.md) FR-014）

---

## 5. Definition Details（定義内容）

### 5.1 Entity Definition and ER Diagram（エンティティ定義・ER図）

#### Entity List（エンティティ一覧）

| Entity Name（エンティティ名） | Description（説明） |
|---|---|
| Processing Date Folder（処理日フォルダ） | `Bot News/YYYY-MM-DD/`。日付は初回のBot処理日（JST）。記事公開日ではない |
| Article Markdown（記事Markdown） | 1記事＝1 Markdownファイル。最終記事URLで一意に識別する |

#### ER Diagram（ER図）

```text
Obsidian Vault（絶対パス: O-06）
└── Bot News/
    └── YYYY-MM-DD/                              ← 初回のBot処理日（JST）
        ├── 記事タイトル.md
        └── 記事タイトル_<URL由来短縮識別子>.md   ← 同名・別の最終記事URLの場合

Processing Date Folder 1 ──── 0..n Article Markdown
Article Markdown 1 ──── 1 最終記事URL（一意キー）
```

- カテゴリ別サブフォルダは作成しない
- Obsidian Vault 自体を Git Repository 内へ保存しない
- 記事Markdownは、再処理されても初回処理日フォルダから移動・複製しない

#### Folder Date Example（日付フォルダの例）

```text
published: 2026-10-05
processed: 2026-10-06

保存先: Bot News/2026-10-06/
```

### 5.2 Table Definitions（テーブル定義）

本Botはデータベースを使用しない。テーブル定義の代わりに、記事Markdownの構成・ファイル規則・一意規則・更新規則を定義する。

#### YAML frontmatter（YAML frontmatter）

判定・管理用データは YAML frontmatter へ保存する。基本構造は次を正とする。

```yaml
---
url: https://example.com/news/123
published: 2026-10-06
processed: 2026-10-06

jev_score: 3
jev_audience: beginner
jev_category: AI

human_decision:
human_score:
---
```

初期調整期間中に人間評価を記録した後の例:

```yaml
human_decision: adopted
human_score: 4
```

| Key（キー） | Description（説明） |
|---|---|
| `url` | 最終記事URL。システム上の一意キー。入力URLではない |
| `published` | 記事自体の公開日（JSTの日付） |
| `processed` | 初回のBot処理日（JST）。再処理しても変更しない |
| `jev_score` | Jevの指導有用度Score（0〜4） |
| `jev_audience` | Jevが判定した対象レベル（`beginner` / `intermediate` / `other`） |
| `jev_category` | Jevが判定した記事カテゴリ。単一値。配列にしない（候補の分類体系は O-01） |
| `human_decision` | 人間評価の採否（`adopted` / `rejected`）。未評価の場合は空 |
| `human_score` | 人間評価のScore（0〜4。Jevと同じ5段階）。未評価の場合は空 |

- `published` と `processed` は別属性として保持する
- `jev_*` と `human_*` は独立データとして保持し、互いに上書きしない
- 値の定義は [02_REQUIREMENTS_DEFINITION.md](./02_REQUIREMENTS_DEFINITION.md) §5.1 を正とする

#### Markdown Body（Markdown本文）

YAML frontmatter とは別に、本文には少なくとも次を読みやすいMarkdownとして配置する。

| Element（要素） | Description（説明） |
|---|---|
| 記事タイトル | 記事のタイトル |
| 記事URL | 最終記事URL |
| 公開日 | 記事公開日 |
| Jev判定の人間向け表示 | 指導有用度Score・対象レベル・記事カテゴリを、人が読める形で示す |
| 記事冒頭 | 記事本文の先頭部分。保存量は O-02 |

- 同じ管理情報を無意味に何度も複製しない
- 記事全文は保存しない

#### File Name Rules（ファイル名規則）

| Case（条件） | File Name（ファイル名） |
|---|---|
| 通常 | `記事タイトル.md` |
| 同一処理日フォルダ内に同じファイル名が既にあり、最終記事URLが異なる | `記事タイトル_<URL由来短縮識別子>.md` |

例:

```text
AI時代の働き方_ab12cd.md
```

- 最終記事URLが異なる記事は、タイトルが同じでも別記事として扱う
- 同じタイトルであることを理由に既存記事を上書きしない
- URL由来短縮識別子の生成方式は未決（実装段階で決定）

#### URL Uniqueness Rules（URL一意規則）

| Case（条件） | Behavior（処理） |
|---|---|
| 未登録の最終記事URL | 当日の処理日フォルダへ新規Markdownを作成する |
| 登録済みの最終記事URL | 既存Markdownを特定し、新しいファイルを作成せず既存Markdownを更新する（再処理） |

- 一意キーは最終記事URLである。Googleニュース等の入力URLは一意キーにしない
- 入力URLが異なっても、最終記事URLが同じであれば同一記事として扱う
- 別の日に同じ記事を入力しても、新しい処理日フォルダへ移動・複製しない
- 既存Markdownの検索方式と最終記事URLの正規化方式（追跡用Query Parameter等の扱いを含む）は O-04（[05_ARCHITECTURE_DESIGN.md](./05_ARCHITECTURE_DESIGN.md)）で管理する

#### Reprocessing Update Rules（再処理時の更新規則）

再処理は、登録済みの最終記事URLが入力され、対象日判定を通過した場合のみ行う。対象外の場合は既存Markdownを更新しない。

| Item（項目） | Behavior（再処理時の扱い） |
|---|---|
| 記事タイトル | 最新の取得結果へ更新する |
| 記事冒頭 | 最新の取得結果へ更新する |
| `jev_score` / `jev_audience` / `jev_category` | 最新の判定結果へ更新する |
| `processed` | 初回処理日を保持する |
| `human_decision` / `human_score` | 保持する。削除・初期化・上書きしない |
| 保存先フォルダ | 初回処理日フォルダのまま |

例:

```text
初回処理: 2026-10-06
保存先:   Bot News/2026-10-06/article.md

2026-10-07 に同じ記事を再入力して再判定
→ processed: 2026-10-06 を維持
→ ファイルは Bot News/2026-10-06/ に残す
```

再処理の判断規則の正本は [02_REQUIREMENTS_DEFINITION.md](./02_REQUIREMENTS_DEFINITION.md) §5.1.5 である。

### 5.3 Data Access and Role Design（データアクセス権限・ロール設計）

| Role Name（ロール名） | Accessible Data / Permitted Operations（アクセス可能なデータ / 操作範囲） |
|---|---|
| 利用者（Repository管理者本人） | Obsidian上で記事Markdownを参照する。初期調整期間は人間評価を記録する（入力方法は O-03） |
| Bot | `Bot News/` 配下で、処理日フォルダと記事Markdownを作成し、登録済みの記事Markdownを再処理時の更新規則に従って更新する |

利用者アカウントや複数利用者の権限区分は要求されていない。

### 5.4 Personal and Confidential Data Policy（個人情報・機密データの取り扱い方針）

- 本Botの処理対象は公開されたニュース記事であり、個人情報の収集を目的としない
- Jev利用のための APIキー等の認証情報は機密データとして扱う
- 認証情報を Git へ commit しない。設計書・README に実値を書かない
- 認証情報の具体的な保存方式は未決（実装段階で決定）。決定前に AI判断で `.env` 等の保存方式を実装しない

### 5.5 Encryption, Masking, and Logging Policy（暗号化・マスキング・ログ取得方針）

| Type（種別） | Target（対象） | Policy / Method（方式・方針） |
|---|---|---|
| Encryption（暗号化） | 記事Markdown | 本文書では対象外。理由: ローカルのObsidian Vaultへの保存であり、暗号化要件の指定がないため |
| Masking（マスキング） | なし | 本文書では対象外。理由: マスキング要件の指定がないため |
| Logging（ログ取得） | なし | 本文書では対象外。理由: ログ取得要件の指定がないため |

### 5.6 Security Design Specifications（セキュリティ設計仕様）

| Type（種別） | Design Specification（設計仕様） |
|---|---|
| Authentication（認証） | Jev利用時の認証情報は Git・設計書・README に含めない。保存方式は未決（実装段階で決定） |
| Authorization（認可） | 本文書では対象外。理由: 単一利用者のローカル実行であり、利用者アカウント機能が要求されていないため |
| Access Control（権限管理） | Botの書込み先は Obsidian Vault の `Bot News/` 配下とする。Vault の絶対パスは O-06 |
| Communication（通信） | 最終記事URLの取得、記事情報取得、Jev判定で外部と通信する。方式は [05_ARCHITECTURE_DESIGN.md](./05_ARCHITECTURE_DESIGN.md) で管理する |
| Data Storage（データ保存） | 記事Markdownを Obsidian Vault へ保存する。Vault を Git Repository 内に置かない。記事全文を保存しない |
| Data Disposal（データ廃棄） | Jev Score を理由に記事を自動破棄しない。記録済みの人間評価は、日常入力の終了後も削除しない。過去データを一括削除しない |
| Personal Data Protection（個人情報保護） | §5.4 に従う |

---

## 6. Open Issues（未決事項）

| ID | Open Issue（未決事項） | Owner（担当者） | Due Date（期限） | Status（ステータス） |
|---|---|---|---|---|
| O-02 | 記事冒頭の保存量。何文字保存するか | Takashi Oikawa | 未定 | OPEN |
| O-06 | Obsidian Vault の絶対パス。保存先フォルダ名 `Bot News` は確定しており、Mac上の Vault 絶対パスが未決 | Takashi Oikawa | 未定 | OPEN |

#### Implementation-Stage Items（実装段階で決定する事項）

以下は本文書で確定しない。実装段階で決定する。

| Item（項目） | Related Section（関連箇所） |
|---|---|
| URL由来短縮識別子の生成方式 | §5.2 File Name Rules |
| Jev認証情報（APIキー）の具体的保存方式 | §5.4 / §5.6 |

---

## 7. Handoff to Detail Design（詳細設計への引き継ぎ）

- 一意キーは最終記事URLであり、frontmatter の `url` に保存する。入力URLを一意キーにしない
- 保存先日付フォルダと `processed` は初回処理日で決まり、再処理しても変えない
- 再処理では記事タイトル・記事冒頭・`jev_*` だけを更新し、`human_*` を保持する
- 同じタイトルでも最終記事URLが異なれば別記事である。既存ファイルを上書きしない
- 記事全文と秘密情報を保存・commitしない
