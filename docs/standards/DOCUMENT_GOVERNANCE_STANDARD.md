<!--
Program Name: Document Governance Standard
Language: Markdown
Function: 全Markdown文書の共通Document Infoヘッダー正本とGovernance検証資産の配布規則を定める
Created: 2026-09-05
Last Updated: 2026-10-08
Author: Takashi Oikawa
AI: Cursor Grok 4.6
Memo: 設計文書固有規則はDESIGN_DOCUMENT_STANDARD.mdを正とする。User向け表示項目の併記形式は本文書§5.6を正とする
-->

# Document Governance Standard（文書ガバナンス標準）

<!-- Document Info（文書情報） -->
| Item（項目） | Value（値） |
|---|---|
| Document ID（文書ID） | STD-DOC-GOVERNANCE-001 |
| Version（バージョン） | 1.7 |
| Status（ステータス） | Approved |
| Created Date（作成日） | 2026-09-05 |
| Last Updated（最終更新日） | 2026-10-08 |
| Owner（管理者） | Takashi Oikawa |
| Related Documents（関連文書） | `/CONSTITUTION.md` / `/AGENTS.md` / `solacom_main/docs/standards/DESIGN_DOCUMENT_STANDARD.md` / `solacom_main/docs/standards/DOCUMENT_HISTORY_RULE.md` / `solacom_main/docs/standards/SPEC_VERSION_HEADER_SPEC.md` |
| Source Location（正本配置） | `solacom_main/docs/standards/DOCUMENT_GOVERNANCE_STANDARD.md` |

---

## Table of Contents（目次）

1. [Purpose（目的）](#1-purpose目的)
2. [Scope（対象範囲）](#2-scope対象範囲)
3. [Out of Scope（対象外範囲）](#3-out-of-scope対象外範囲)
4. [Assumptions（前提条件）](#4-assumptions前提条件)
5. [Definition Details（定義内容）](#5-definition-details定義内容)
   - [5.6 Bilingual Display Rule（日本語・英語併記規則）](#56-bilingual-display-rule日本語英語併記規則)
6. [Open Issues（未決事項）](#6-open-issues未決事項)
7. [Handoff to Detail Design（詳細設計への引き継ぎ）](#7-handoff-to-detail-design詳細設計への引き継ぎ)

---

## 1. Purpose（目的）

本文書は、全 Markdown 文書に共通する Document Info ヘッダー項目の正本である。あわせて、Template Repository における必須ヘッダー検査の機械実行方法を定める。

設計文書固有の構成・README 規則・本文セクション・バージョン意味・ステータス意味は `DESIGN_DOCUMENT_STANDARD.md` を正とする。YAML フロントマターは `SPEC_VERSION_HEADER_SPEC.md` を正とする。本文書はこれらの設計固有規則および YAML 規約を再定義しない。

---

## 2. Scope（対象範囲）

| Target（対象） | Description（内容） |
|---|---|
| Header Canonical（ヘッダー正本） | 全 Markdown 文書に共通する Document Info 項目名 |
| Applicable Repository（適用リポジトリ） | 本標準を導入したリポジトリ、および Template Repository から作成したリポジトリ |
| Inspection Target（検査対象） | Repository 内の管理対象 Markdown 全体（`.md`）。`docs/` 配下に限定しない |
| Inspection Method（検査方法） | DEVELOPMENT 等の現行 Profile では `scripts/validate-docs.py` および GitHub Actions。LEARNING Profile では必須としない |

検査対象の例（限定列挙ではない）:

- `README.md`
- `docs/` 配下の Markdown
- `project-notes/CURRENT.md`
- `project-notes/` 配下の Markdown

---

## 3. Out of Scope（対象外範囲）

- `/CONSTITUTION.md` および `/AGENTS.md` の本文改訂。両ファイルは中央正本の管理コピーであり、`LOCAL_EDIT_POLICY: PROHIBITED`
- 設計文書固有の構成・README 必須ルール・本文共通セクション。これらは `DESIGN_DOCUMENT_STANDARD.md` を正とする
- Created Date / Last Updated / Version の履歴運用。これは `DOCUMENT_HISTORY_RULE.md` を正とする
- YAML フロントマター（`SPEC_VERSION_HEADER_SPEC.md`）の検査。Document Info 表形式の必須ヘッダー検査とは別仕様である

---

## 4. Assumptions（前提条件）

- 本文書の正本は `solacom_main/docs/standards/DOCUMENT_GOVERNANCE_STANDARD.md` である
- Template Repository 側の同パスファイルは、中央正本からの配布コピーであり、正本と IDENTICAL でなければならない
- `/CONSTITUTION.md` と `/AGENTS.md` の中央正本は `solacom_main/docs/standards/project-bootstrap/` である
- Governance検証資産の Canonical Source は `solacom_main/docs/standards/project-bootstrap/` である
- `project-bootstrap` の validator / workflow は Canonical Source ではなく Distribution Copy である
- 設計7文書は初回導入後にプロジェクト固有の設計正本となる（`CONSTITUTION.md` §6.5）。本項は DEVELOPMENT 等の現行 Profile に適用する。LEARNING には適用しない
- User向け表示項目の正式形式は English（日本語）である

---

## 5. Definition Details（定義内容）

### 5.1 Central SSOT Reference（中央正本参照）

`/CONSTITUTION.md` および `/AGENTS.md` は、次の中央正本を参照する管理コピーである。

```text
solacom_main/docs/standards/project-bootstrap/CONSTITUTION.md
solacom_main/docs/standards/project-bootstrap/AGENTS_SOURCE.md
```

管理ヘッダ:

```text
DISTRIBUTION_MODE: COPY_FROM_CENTRAL_SSOT
LOCAL_EDIT_POLICY: PROHIBITED
```

各リポジトリ側で両ファイルを独自編集してはならない。更新は中央正本の変更工程と配布手順に従う。

本文書の配布コピーも、次を正本とする。

```text
solacom_main/docs/standards/DOCUMENT_GOVERNANCE_STANDARD.md
```

### 5.2 Required Document Info Headers（必須ヘッダー）

Repository 内の管理対象 Markdown 文書は、次の共通項目を Document Info として持つ。本表が全文書共通ヘッダーの正本である。

| Item Name（項目名） | Description（説明） |
|---|---|
| Document ID（文書ID） | 一意の識別子（例: `REQ-001`, `ARCH-001`） |
| Version（バージョン） | セマンティックバージョニング |
| Status（ステータス） | Draft / Review / Approved / Deprecated |
| Created Date（作成日） | 文書の初版作成日（ISO 8601形式: `YYYY-MM-DD`） |
| Last Updated（最終更新日） | 直近の更新日（ISO 8601形式: `YYYY-MM-DD`） |
| Owner（管理者） | 文書の責任者氏名 |
| Related Documents（関連文書） | 参照する設計書・仕様書のリスト |

設計文書における Version および Status の**値**の値域は `DESIGN_DOCUMENT_STANDARD.md` 第9章・第10章に従う。項目名の正本は本文書である。値（`Draft` / `Approved` / `1.0` 等）は並び替えない。

表示項目名の正式形式は English（日本語）である。詳細は §5.6 を正とする。

Validator は、上記 **項目名文字列が文書内に存在すること** を検査する。項目値の妥当性判定、本文セクション構成の検査、履歴規則の検査は対象外とする。English（日本語）を Legacy 扱いしない。

### 5.3 Document Validator（文書検査）

検査コマンド:

```bash
python3 scripts/validate-docs.py
```

管理対象Markdown:

```text
Repository内のMarkdown
－ 明示除外
－ Git ignored Markdown
```

検査対象:

- Repository 内の `.md` ファイルを原則として検査する
- `docs/**/*.md` への固定は行わない
- untracked かつ Git ignore されていない Markdown は検査対象とする
- tracked な Markdown は検査対象とする
- Git ignored Markdown は検査対象外とする

Git ignore判定:

- Git 自身の ignore ルールを使用する
- 判定は `git check-ignore` による。`--no-index` は使用しない
- tracked file は ignore pattern に一致していても検査対象として残す
- 対象となる ignore 定義には、Repository で有効な次を含む

```text
.gitignore
.git/info/exclude
その他 Git が check-ignore で認識するignore規則
```

- `.specs/` のような Repository 固有パスを中央標準の固定除外一覧へ追加しない
- Git ignore 状態を正常に判定できない場合、validator は FAIL として終了する。対象ファイルを黙って skip してはならない

Git ignore状態と検査対象:

```text
untracked + not ignored
→ 検査対象

untracked + ignored
→ 検査対象外

tracked
→ 検査対象
```

明示除外:

| Path（パス） | Reason（理由） |
|---|---|
| `/AGENTS.md` | 中央正本の管理コピー。Document Info 表形式ではない |
| `/CONSTITUTION.md` | 中央正本の管理コピー。Document Info 表形式ではない |
| `.git/` | Git 内部領域 |
| `.venv/` | 依存領域（`SPEC_VERSION_HEADER_SPEC.md` §2.3） |
| `.venv_docgen/` | 依存領域（`SPEC_VERSION_HEADER_SPEC.md` §2.3） |
| `node_modules/` | 依存領域（`SPEC_VERSION_HEADER_SPEC.md` §2.3） |
| `target/` | 生成領域（`SPEC_VERSION_HEADER_SPEC.md` §2.3） |

判定:

| Result（結果） | Condition（条件） |
|---|---|
| PASS | 対象ファイルが1件以上存在し、各ファイルが必須ヘッダー項目名をすべて含む |
| FAIL | 対象ファイルが0件、または1件以上のファイルで必須ヘッダー項目名が欠ける |

終了コード:

- `0`: 全件 PASS
- `1`: 1件以上 FAIL

### 5.4 GitHub Actions

`.github/workflows/validate-docs.yml` が `push` および `pull_request` で `scripts/validate-docs.py` を実行する。

### 5.5 Governance Validation Asset Distribution（検証資産配布）

Governance検証資産は必須Governance文書10とは別分類である。DEVELOPMENT 等の現行 Profile では次の 2 件を必須とする。LEARNING Profile では必須としない。LEARNING 導入時には配布しない。既に存在する validator / workflow は自動削除しない。

```text
/scripts/validate-docs.py
/.github/workflows/validate-docs.yml
```

Canonical Source:

```text
solacom_main/docs/standards/project-bootstrap/scripts/validate-docs.py
solacom_main/docs/standards/project-bootstrap/.github/workflows/validate-docs.yml
```

Distribution Copy:

```text
project-bootstrap/scripts/validate-docs.py
project-bootstrap/.github/workflows/validate-docs.yml
```

Runtime Artifact:

```text
<repository>/scripts/validate-docs.py
<repository>/.github/workflows/validate-docs.yml
```

Source → Target Mapping:

```text
docs/standards/project-bootstrap/scripts/validate-docs.py
→ project-bootstrap/scripts/validate-docs.py
→ Runtime /scripts/validate-docs.py

docs/standards/project-bootstrap/.github/workflows/validate-docs.yml
→ project-bootstrap/.github/workflows/validate-docs.yml
→ Runtime /.github/workflows/validate-docs.yml
```

管理メタデータ（コメント形式）:

```text
STANDARD_ID
STANDARD_VERSION
SOURCE
DISTRIBUTION_MODE: COPY_FROM_CENTRAL_SSOT
LOCAL_EDIT_POLICY: PROHIBITED
```

初版:

```text
validate-docs.py
STANDARD_ID: SCAO-DOC-VALIDATOR
STANDARD_VERSION: 1.0

validate-docs.yml
STANDARD_ID: SCAO-DOC-VALIDATOR-WORKFLOW
STANDARD_VERSION: 1.0
```

Canonical Source と Distribution Copy / Runtime Artifact は `cmp` による完全一致を必須とする。不一致は Drift である。自動修正しない。各リポジトリ側での Local Edit は禁止する。

中央SSOT更新直後の既存Repositoryとの版差は Planned Migration Drift として扱う。Repository単位Migration完了まで許容する。

### 5.6 Bilingual Display Rule（日本語・英語併記規則）

管理対象 Markdown のUser向け表示項目は、次を正式形式とする。

```text
English（日本語）
```

例:

```text
Document Info（文書情報）
Item（項目）
Value（値）

Document ID（文書ID）
Version（バージョン）
Status（ステータス）
Created Date（作成日）
Last Updated（最終更新日）
Owner（管理者）
Related Documents（関連文書）

Purpose（目的）
Scope（対象範囲）
Required（必須）
Standard（標準）
Optional（任意）
Not Required（必須ではない）
```

次の形式は新規作成および改修箇所で使用してはならない。

```text
文書情報（Document Info）
項目（Item）
目的（Purpose）
日本語（English）
```

適用対象:

- 文書タイトル
- 見出し
- 表の列名
- 表の項目名
- ラベル
- Document Info（文書情報）の表示項目
- 目次の表示名
- 文書内で正式名称として使用する項目名

適用対象外（翻訳・並び替えを行わない）:

```text
ファイル名
directory名
path
コマンド
CLI option
コード
変数名
関数名
class名
API名
Document ID値
STANDARD_ID
Purpose正式値
Status正式値
Version値
Git branch名
Repository名
URL
外部製品・サービス固有名称
```

例として、次はそのままとする。

```text
LEARNING
DEVELOPMENT
Draft
Approved
--purpose LEARNING
docs/design/
AGENTS.md
```

正本は本文書である。中央標準・Template・Repository固有管理文書は本文書を参照する。同一ルールを複数文書で独自定義してはならない。

既存の English（日本語）は正式形式である。Legacy として扱わない。

`日本語（English）` が残る既存箇所があれば Planned Migration とする。一括置換は禁止する。Repository単位・文書単位で Migration する。

Validator は §5.2 の English（日本語）項目名を正式形式として検査する。既存正式形式を Legacy 扱いしない。日本語先行形式との二重許容は行わない。

---

## 6. Open Issues（未決事項）

本文書では対象外。理由: 全文書共通の必須ヘッダー項目は本章で正本化し、追加の未決事項はない。

---

## 7. Handoff to Detail Design（詳細設計への引き継ぎ）

- 検査対象は Repository 内の管理対象 Markdown 全体とする。`docs/**/*.md` に固定しない
- 管理対象は、明示除外および Git ignored Markdown を除いた Repository 内 Markdown とする
- Git ignore 判定は `git check-ignore` を使用する。判定不能時は FAIL とする
- Repository 固有パスを中央標準の固定除外一覧へ追加しない
- `README.md` および `project-notes/` 配下の Markdown は、明示除外または Git ignored でない限り検査対象に含める
- 必須ヘッダー項目名は本文書 §5.2 の表記（English（日本語））と同一文字列にする
- User向け表示項目の併記形式は本文書 §5.6 を正とする。他文書で独自定義しない
- `/CONSTITUTION.md` と `/AGENTS.md` は検査対象外（配置がリポジトリ直下であり、ヘッダ形式が異なる）
- Governance検証資産は Canonical Source から明示 Mapping で配布する。Local Edit は禁止する。LEARNING Profile では必須とせず、導入時に配布しない
- 設計文書固有規則は `DESIGN_DOCUMENT_STANDARD.md` を参照する。同標準は DEVELOPMENT Repository 向けであり、LEARNING へ無条件適用しない
