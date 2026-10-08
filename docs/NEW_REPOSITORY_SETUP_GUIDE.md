<!--
Program Name: New Repository Setup Guide
Language: Markdown
Function: project-bootstrapを使う新規Repository作成の詳細手順を、Template経路とLEARNING経路に分けて案内する
Created: 2026-09-24
Last Updated: 2026-10-08
Author: Takashi Oikawa
AI: Cursor Grok 4.7
Memo: 新規作成のみを扱う。Existing RepositoryのMigrationとD-016 Step 15は対象外。Version 1.0は初回Approved版
-->

# New Repository Setup Guide（新規Repository作成手順）

<!-- Document Info（文書情報） -->
| Item（項目） | Value（値） |
|---|---|
| Document ID（文書ID） | PB-SETUP-001 |
| Version（バージョン） | 1.0 |
| Status（ステータス） | Approved |
| Created Date（作成日） | 2026-09-24 |
| Last Updated（最終更新日） | 2026-10-08 |
| Owner（管理者） | Takashi Oikawa |
| Related Documents（関連文書） | [README.md](../README.md) / [CONSTITUTION.md](../CONSTITUTION.md) / [AGENTS.md](../AGENTS.md) / [CURRENT.md](../project-notes/CURRENT.md) / [DOCUMENT_GOVERNANCE_STANDARD.md](./standards/DOCUMENT_GOVERNANCE_STANDARD.md) |

---

## 1. Purpose（目的）

本Guideは、`project-bootstrap` を使って新規Repositoryを作成するUser向けの詳細手順書である。

扱う範囲は次のとおりである。

- 新規Repositoryの作成方法
- Purpose別の作成経路
- 作成後の初期化
- Governance確認
- 検証
- commit / push 前確認

Existing Repositoryへの移行手順は扱わない。D-016 Step 15 Existing Repository Individual Adoption（既存Repository個別導入）は別運用であり、本Guideへ統合しない。

---

## 2. Before You Start（開始前確認）

最初に、Userが Repository の Purpose（目的）を確定する。

正式値は次の5値である。1 Repository = 1 Primary Purpose とする。

```text
GOVERNANCE
DISTRIBUTION
DEVELOPMENT
LEARNING
EXPERIMENT
```

AI および installer は、Repository の内容から Purpose を推測してはならない。Purpose の確定権限はUserにある。

確定後、`Purpose = LEARNING` か否かで経路を分ける。

---

## 3. Route Selection（経路選択）

`GOVERNANCE` / `DISTRIBUTION` / `DEVELOPMENT` / `EXPERIMENT` は Template Route（Template経路）である。

```text
GOVERNANCE
DISTRIBUTION
DEVELOPMENT
EXPERIMENT
        ↓
Template Route
        ↓
project-bootstrap
        ↓
Use this template
```

`LEARNING` は LEARNING Route（LEARNING経路）である。

```text
LEARNING
        ↓
LEARNING Route
        ↓
README.mdを持つ新規Repository
        ↓
install-project-standards.sh --purpose LEARNING
```

LEARNING では `project-bootstrap` の `Use this template` を使用しない。LEARNING 用の別 Template Repository は作成しない。

---

## 4. Template Route（Template経路）

対象は次である。

```text
GOVERNANCE
DISTRIBUTION
DEVELOPMENT
EXPERIMENT
```

### 4.1 Create Repository（Repository作成）

GitHub の `project-bootstrap` から、次を使用する。

```text
Use this template
→ Create a new repository
```

Repository 名と公開範囲は、対象プロジェクトの要件に従う。本Guideでは固定しない。

### 4.2 Clone Repository（Clone）

作成した Repository を local へ clone する。

clone URL と local directory はUser環境に依存する。本Guideでは固定値を書かない。

### 4.3 Verify Git State（Git状態確認）

作業開始前に、Repository root で次を確認する。

```bash
git status
git branch --show-current
git rev-parse HEAD
git rev-parse origin/main
git log -1 --oneline
```

確認する状態は次である。

```text
Repository rootであること
Branchがmainであること
HEADとorigin/mainの同期状態
未commit差分の有無
```

作業 Branch は `main` を前提とする。

Remote の最新性を確認する必要がある場合は、次を実行したあと、`origin/main` を再確認する。

```bash
git fetch origin
```

`HEAD = origin/main` という表示だけで、Remote が最新であると断定しない。`git fetch origin` の前の `origin/main` は、local が最後に取得した Remote 参照である。

想定外の状態があれば、初期化作業へ進まず停止する。

### 4.4 Read Governance Documents（Governance文書確認）

Template Route では、作業開始前に Governance 導入ゲートを確認する。1件でも不足している場合は、Repository 固有 README や設計文書の初期化へ進まず停止する。

#### Required Governance Documents（必須Governance文書）

10件である。

```text
/CONSTITUTION.md
/AGENTS.md
/CHANGELOG.md
/docs/design/README.md
/docs/design/01_REQUEST_DEFINITION.md
/docs/design/02_REQUIREMENTS_DEFINITION.md
/docs/design/03_DATA_AND_SECURITY_DESIGN.md
/docs/design/04_UI_AND_FLOW_DESIGN.md
/docs/design/05_ARCHITECTURE_DESIGN.md
/docs/design/06_OPERATION_AND_HANDOFF.md
```

#### Governance Validation Assets（Governance検証資産）

2件である。

```text
/scripts/validate-docs.py
/.github/workflows/validate-docs.yml
```

`project-notes/CURRENT.md` は Standard（標準）である。必須 Governance 文書10には追加しない。

#### Reading（読込）

読込は `AGENTS.md` の規則に従う。独自の読込順序は新設しない。

`CURRENT.md` が存在するため、Purpose 別の Required Reading Order（必読順）より前に `CURRENT.md` を確認し、Git の実状態と照合する。

その後、DEVELOPMENT and Others（DEVELOPMENT等）の Required Reading Order に従って、次を確認する。

```text
CONSTITUTION.md
docs/design/README.md
docs/design/01_REQUEST_DEFINITION.md
docs/design/02_REQUIREMENTS_DEFINITION.md
docs/design/03_DATA_AND_SECURITY_DESIGN.md
docs/design/04_UI_AND_FLOW_DESIGN.md
docs/design/05_ARCHITECTURE_DESIGN.md
docs/design/06_OPERATION_AND_HANDOFF.md
```

### 4.5 Initialize README（README初期化）

Template からコピーされた `README.md` を、その Repository 固有 README へ変更する。

`project-bootstrap` の説明をそのまま残してはならない。

Repository 固有 README には、次が分かる内容を記載する。

- Repository の目的
- 概要
- 主な機能または役割
- 利用方法
- 正本文書への入口

Document Info（文書情報）は維持し、Repository 固有の値へ更新する。

### 4.6 Initialize CURRENT.md（CURRENT.md初期化）

`project-notes/CURRENT.md` を Repository 固有状態へ更新する。

管理対象は次である。

```text
Purpose（目的）
Completed（完了）
Current（現在）
Next（次）
Blockers（阻害要因）
Related Decisions（関連Decision）
```

`CURRENT.md` は必須 Governance 文書10へ追加しない。Governance Validation Assets へも追加しない。

Runtime 側に `CURRENT_TEMPLATE.md` を作成してはならない。

### 4.7 Initialize Design Documents（設計文書初期化）

`docs/design/` 配下の7文書を、Template の説明のまま残さず、Repository 固有内容へ更新する。

次の中央管理コピー、および配布コピーは、Repository 固有内容へ書き換えない。

```text
CONSTITUTION.md
AGENTS.md
docs/standards/DOCUMENT_GOVERNANCE_STANDARD.md
```

### 4.8 CHANGELOG Handling（CHANGELOG取扱い）

Template 内の `CHANGELOG.md` は、`project-bootstrap` 上では Distribution Template Artifact（配布用Template成果物）である。`project-bootstrap` 自身の変更履歴正本ではない。

新規 Repository へ配布された後は、Runtime `/CHANGELOG.md` として、その Repository の変更履歴正本に使用する。

`project-bootstrap` 自身の履歴と混同しない。

### 4.9 Validate Documents（文書検証）

Repository root で次を実行する。

```bash
python3 scripts/validate-docs.py
```

PASS だけで Semantic Compliance（意味準拠）の完了とは判断しない。

併せて次を確認する。

```bash
git diff --check
git status --short
```

差分内容をレビューする。

### 4.10 Commit and Push（commit・push）

commit と push は自動では行わない。

```text
差分レビュー
→ User確認
→ Userの明示指示
→ commit
→ push
```

push 後は、GitHub Actions の `Validate Documents` の結果を確認する。

---

## 5. LEARNING Route（LEARNING経路）

この経路は、Userが Purpose を明示的に `LEARNING` と確定した場合のみ使用する。

### 5.1 Create Repository（Repository作成）

`project-bootstrap` の `Use this template` は使用しない。

新規 Repository を用意し、root に `README.md` を作成する。`README.md` が存在しなければ、installer は停止する。installer は `README.md` を作成しない。

### 5.2 Clone Repository（Clone）

作成した Repository を local へ clone する。

導入対象の directory は、Git Repository の root でなければならない。

### 5.3 Dry Run（事前確認）

中央正本 `solacom_main` の次の script を使用する。

```text
docs/standards/scripts/install-project-standards.sh
```

環境依存の絶対 path は固定しない。形式は次のとおりである。

```bash
<solacom_main>/docs/standards/scripts/install-project-standards.sh \
  --purpose LEARNING \
  --dry-run \
  /absolute/path/to/target-repository
```

Dry Run ではファイルを変更しない。表示された結果を確認する。

### 5.4 Execute Installation（導入実行）

Dry Run の確認後、Userが実行を承認した場合のみ実実行する。

```bash
<solacom_main>/docs/standards/scripts/install-project-standards.sh \
  --purpose LEARNING \
  /absolute/path/to/target-repository
```

LEARNING で配置される標準は次の3件である。

```text
/CONSTITUTION.md
/AGENTS.md
/project-notes/CURRENT.md
```

`README.md` は installer が作成せず、上書きもしない。

### 5.5 Not Installed for LEARNING（LEARNINGで配布しないもの）

次は LEARNING の導入単位ではない。

```text
/CHANGELOG.md
/docs/design/*
/scripts/validate-docs.py
/.github/workflows/validate-docs.yml
```

これらの不存在を Governance 欠落として扱わない。既に存在するものを、installer が自動削除するという意味ではない。

### 5.6 Initialize CURRENT.md（CURRENT.md初期化）

配布された `project-notes/CURRENT.md` を、Repository 固有状態へ更新する。

### 5.7 Verify Result（結果確認）

最低限、次で導入結果を確認する。

```bash
git status --short
```

LEARNING では validator と workflow は必須ではない。`python3 scripts/validate-docs.py` は、この経路の必須手順にしない。

### 5.8 Commit and Push（commit・push）

Template Route と同じ順とする。

```text
差分レビュー
→ User確認
→ Userの明示指示
→ commit
→ push
```

---

## 6. Do Not Modify（変更禁止）

新規 Repository を初期化するとき、次の中央管理コピーを独自編集しない。

```text
CONSTITUTION.md
AGENTS.md
docs/standards/DOCUMENT_GOVERNANCE_STANDARD.md
```

Repository 固有の情報は、README、`CURRENT.md`、設計文書など、適切な Repository 固有文書へ記録する。

---

## 7. Completion Check（完了確認）

### Template Route（Template経路）

最低限、次を確認する。

```text
Purpose確定済み
必須Governance文書10 存在確認済み
Governance Validation Assets 2 存在確認済み
HEAD / origin/main 同期状態確認済み
README Repository固有化済み
CURRENT.md 初期化済み
設計文書 Repository固有化済み
中央管理コピー未改変
validator PASS
git diff --check PASS
差分レビュー済み
User明示承認後 commit / push
GitHub Actions Validate Documents確認
```

### LEARNING Route（LEARNING経路）

最低限、次を確認する。

```text
Purpose = LEARNING 明示済み
README.md 存在
CONSTITUTION.md 配置済み
AGENTS.md 配置済み
project-notes/CURRENT.md 配置済み
READMEをinstallerが変更していない
CURRENT.md 初期化済み
不要なdocs/design等を必須扱いしていない
差分レビュー済み
User明示承認後 commit / push
```

---

## 8. Out of Scope（対象外）

本Guideでは次を扱わない。

```text
Existing Repository Migration
Existing Repositoryへの一括Governance導入
Repository rename
Repository move
Repository archive
Repository delete
D-016再設計
D-017再設計
D-018再設計
Central Governance更新手順
```
