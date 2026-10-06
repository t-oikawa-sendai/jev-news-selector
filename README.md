<!--
Program Name: project-bootstrap README
Language: Markdown
Function: Template Repositoryの入口。project-bootstrapの説明と、Template作成直後の利用者案内を兼ねる
Created: 2026-09-24
Last Updated: 2026-09-24
Author: Takashi Oikawa
AI: Cursor Grok 4.7
Memo: Document Infoは本文の表を正とする。Use this template後はRepository固有READMEへ更新する
-->

# project-bootstrap

<!-- Document Info（文書情報） -->
| Item（項目） | Value（値） |
|---|---|
| Document ID（文書ID） | PB-README-001 |
| Version（バージョン） | 1.0 |
| Status（ステータス） | Approved |
| Created Date（作成日） | 2026-09-24 |
| Last Updated（最終更新日） | 2026-09-24 |
| Owner（管理者） | Takashi Oikawa |
| Related Documents（関連文書） | [CONSTITUTION.md](./CONSTITUTION.md) / [AGENTS.md](./AGENTS.md) / [project-notes/CURRENT.md](./project-notes/CURRENT.md) / [docs/NEW_REPOSITORY_SETUP_GUIDE.md](./docs/NEW_REPOSITORY_SETUP_GUIDE.md) / [docs/standards/DOCUMENT_GOVERNANCE_STANDARD.md](./docs/standards/DOCUMENT_GOVERNANCE_STANDARD.md) |

> **Initial README（初期README）**
>
> このREADMEは project-bootstrap の利用案内を兼ねる初期READMEである。
>
> Use this template で新規Repositoryを作成した後は、新しいRepositoryの目的・機能・利用方法を示す Repository固有READMEへ更新する。

---

## Table of Contents（目次）

1. [Overview（概要）](#1-overview概要)
2. [Purpose（目的）](#2-purpose目的)
3. [Role（役割）](#3-role役割)
4. [Features（機能）](#4-features機能)
5. [Benefits（利用効果）](#5-benefits利用効果)
6. [Distributed Assets（配布資産）](#6-distributed-assets配布資産)
7. [Repository Purpose Routes（Purpose別作成経路）](#7-repository-purpose-routespurpose別作成経路)
8. [Quick Start（クイックスタート）](#8-quick-startクイックスタート)
9. [Operational Flow（運用フロー）](#9-operational-flow運用フロー)
10. [Canonical Source（正本との関係）](#10-canonical-source正本との関係)
11. [Setup Guide（詳細手順）](#11-setup-guide詳細手順)

---

## 1. Overview（概要）

`project-bootstrap` は、新しいRepositoryを最初から同じ土台で始めるための雛形である。GitHub Template Repository として使う。

Use this template で新規Repositoryを作ると、次が最初から入る。

- 作業ルールと設計文書の雛形
- 今どこまで進んだかを書く `project-notes/CURRENT.md`
- 文書の基本項目を検査する仕組み

共通ルールの正本は `solacom_main` にある。このRepositoryは、そのルールを新しいRepositoryへ渡す配布用Templateである。Repositoryごとの目的、機能、設計の中身は、利用者と開発者が書く。

---

## 2. Purpose（目的）

Repositoryごとに、同じGovernance基盤を一から作らなくてよいようにする。

- 文書の置き場所の抜けを減らす
- AIごとの独自判断で配置がずれることを減らす
- GitHub上の文書を正本として、作業を続けられるようにする
- Validator と GitHub Actions で、基本的な Document Governance を検査できるようにする

Repository固有の内容は、利用者と開発者が設定する。

---

## 3. Role（役割）

```text
solacom_main
Canonical Source（正本）
        ↓
project-bootstrap
Distribution Template（配布）
        ↓
New Repository
Runtime Artifact（利用側）
```

`solacom_main` が中央正本である。`project-bootstrap` は Distribution Template であり、中央正本ではない。

中央管理コピーは、`project-bootstrap` 側で独自に編集しない。更新は中央標準の更新工程に従う。

---

## 4. Features（機能）

利用者から見た初期状態は、次のとおりである。

- Governance基本文書が最初から置かれる
- 設計文書のTemplateが置かれる
- `CURRENT.md` で、作業の現在地点を管理できる
- Document Validator で、文書の基本項目を検査できる
- GitHub Actions `Validate Documents` が、push と pull request で検査を実行する
- AIの作業ルールが配布される
- 新規Repositoryの初期構成が揃う

---

## 5. Benefits（利用効果）

- 新しいRepositoryのたびに、土台を手で揃える作業が減る
- 必要な文書を置き忘れにくい
- どこに何を書くかを、毎回考えなくてよい
- AIと人間が、同じGovernanceルールを参照できる
- 作業の途中でも、`CURRENT.md` から現在地点を戻しやすい
- push のときに、Document Governance の検査が実行される

---

## 6. Distributed Assets（配布資産）

配布物は次の3分類に分ける。分類をまたいで数えない。

```text
必須Governance文書10
Governance Validation Assets 2
CURRENT.md（Standard / Gate外標準）
```

`.gitignore` はTemplateに含まれる。上の文書分類には含めない。

### Required Governance Documents（必須Governance文書）

10文書である。中央管理コピーと、Repository固有文書を分けて扱う。

| Path（パス） | Kind（種別） | Role（役割） |
|---|---|---|
| [CONSTITUTION.md](./CONSTITUTION.md) | Central Managed Copy（中央管理コピー） | 設計・実装・検証の共通ルール |
| [AGENTS.md](./AGENTS.md) | Central Managed Copy（中央管理コピー） | AIが作業するときの読み順と手順 |
| [CHANGELOG.md](./CHANGELOG.md) | Distribution Template Artifact（配布用Template成果物） | Templateから新規Repositoryへ配布された後、Runtime側の `/CHANGELOG.md` として、そのRepositoryの変更履歴を管理する初期Template。project-bootstrap自身の変更履歴正本ではない |
| [docs/design/README.md](./docs/design/README.md) | Repository-specific Document（Repository固有文書） | 設計文書の入口 |
| [docs/design/01_REQUEST_DEFINITION.md](./docs/design/01_REQUEST_DEFINITION.md) | Repository-specific Document（Repository固有文書） | 何を求めているかの定義 |
| [docs/design/02_REQUIREMENTS_DEFINITION.md](./docs/design/02_REQUIREMENTS_DEFINITION.md) | Repository-specific Document（Repository固有文書） | 満たすべき要件の定義 |
| [docs/design/03_DATA_AND_SECURITY_DESIGN.md](./docs/design/03_DATA_AND_SECURITY_DESIGN.md) | Repository-specific Document（Repository固有文書） | データとセキュリティの設計 |
| [docs/design/04_UI_AND_FLOW_DESIGN.md](./docs/design/04_UI_AND_FLOW_DESIGN.md) | Repository-specific Document（Repository固有文書） | 画面と操作の流れの設計 |
| [docs/design/05_ARCHITECTURE_DESIGN.md](./docs/design/05_ARCHITECTURE_DESIGN.md) | Repository-specific Document（Repository固有文書） | 構成の設計 |
| [docs/design/06_OPERATION_AND_HANDOFF.md](./docs/design/06_OPERATION_AND_HANDOFF.md) | Repository-specific Document（Repository固有文書） | 運用と引き継ぎの設計 |

### Project State（プロジェクト状態）

`CURRENT.md` は Standard（標準）であり、Gate外標準である。必須Governance文書10には加えない。Governance Validation Assets にも加えない。

| Path（パス） | Role（役割） |
|---|---|
| [project-notes/CURRENT.md](./project-notes/CURRENT.md) | 目的、完了、現在地点、次の作業、阻害要因を記録する |

作業を始めた後も、`CURRENT.md` を実状態に合わせて更新する。

### Document Governance（文書Governance）

| Path（パス） | Role（役割） |
|---|---|
| [docs/standards/DOCUMENT_GOVERNANCE_STANDARD.md](./docs/standards/DOCUMENT_GOVERNANCE_STANDARD.md) | 文書ヘッダーと文書検査の共通規則 |

### Validation（検証）

Governance Validation Assets は2件である。必須Governance文書10とは別である。

| Path（パス） | Role（役割） |
|---|---|
| [scripts/validate-docs.py](./scripts/validate-docs.py) | 文書の必須ヘッダーを検査する |
| [.github/workflows/validate-docs.yml](./.github/workflows/validate-docs.yml) | `Validate Documents` として検査を実行する |

### This README（このREADME）

[README.md](./README.md) は、Templateから作成したRepositoryへコピーされる。作成後は、そのRepositoryの目的・機能・利用方法を示す Repository固有READMEへ更新する。

---

## 7. Repository Purpose Routes（Purpose別作成経路）

Purpose は利用者が確定する。AIはRepositoryの内容から Purpose を推測しない。

Purpose の値は次の5つである。ここでは作成経路だけを示す。

```text
GOVERNANCE
DISTRIBUTION
DEVELOPMENT
LEARNING
EXPERIMENT
```

### Template Route（Template経路）

対象は次である。

```text
GOVERNANCE
DISTRIBUTION
DEVELOPMENT
EXPERIMENT
```

```text
project-bootstrap
→ Use this template
→ Create a new repository
```

### LEARNING Route（LEARNING経路）

```text
READMEを持つRepositoryを用意
→ install-project-standards.sh --purpose LEARNING
```

LEARNING では Use this template を使用しない。LEARNING用の別Template Repositoryは作成しない。

---

## 8. Quick Start（クイックスタート）

ここは Template Route の全体像である。対象は `GOVERNANCE` / `DISTRIBUTION` / `DEVELOPMENT` / `EXPERIMENT` である。

Purpose が `LEARNING` のときは、[LEARNING Route（LEARNING経路）](#learning-routelearning経路) に従う。Use this template は使わない。

1. Purpose を利用者が確定する
2. `project-bootstrap` から Use this template を選ぶ
3. 新規Repositoryを作成する
4. clone する
5. README を、そのRepository固有の内容へ更新する
6. `CURRENT.md` を初期化する
7. 設計文書を、そのRepository固有の内容へ更新する
8. validator を実行する
9. 利用者の明示承認後に commit / push する
10. GitHub Actions の `Validate Documents` を確認する
11. 通常の開発を始める

`README.md` と設計文書は、Templateの説明のままにしない。

操作の詳細は [Setup Guide（詳細手順）](#11-setup-guide詳細手順) へ進む。

---

## 9. Operational Flow（運用フロー）

```text
Repository Creation
↓
Repository-specific Initialization
↓
CURRENT.md Initialization
↓
Design Documentation
↓
Local Validation
↓
Review
↓
Commit / Push
↓
GitHub Actions
↓
Normal Development
```

通常の開発に入った後も、`CURRENT.md` を継続して更新する。

---

## 10. Canonical Source（正本との関係）

- 共通Governanceの正本は `solacom_main` である
- `project-bootstrap` は Distribution Template である
- `AGENTS.md` と `CONSTITUTION.md` などの中央管理コピーは、独自に改変しない
- Repository固有の文書と、中央管理コピーを混ぜて扱わない
- 中央標準の更新は、専用の更新工程に従う

---

## 11. Setup Guide（詳細手順）

このREADMEは、全体像と入口を示す。

新規Repository作成の詳細手順は、[NEW_REPOSITORY_SETUP_GUIDE.md](./docs/NEW_REPOSITORY_SETUP_GUIDE.md) を参照する。
