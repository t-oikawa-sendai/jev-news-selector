<!--
Program Name: jev-news-selector README
Language: Markdown
Function: jev-news-selectorのRepository入口。目的・概要・主な機能・利用フロー・設計文書とCURRENT.mdへの入口を示す
Created: 2026-10-06
Last Updated: 2026-10-06
Author: Takashi Oikawa
AI: Cursor
Memo: 設計段階のRepository固有README。記載した機能は設計上の仕様であり未実装。変更履歴はCHANGELOG.md、現在地点はproject-notes/CURRENT.mdを正とする
-->

# jev-news-selector

<!-- Document Info（文書情報） -->
| Item（項目） | Value（値） |
|---|---|
| Document ID（文書ID） | JNS-README-001 |
| Version（バージョン） | 0.1 |
| Status（ステータス） | Draft |
| Created Date（作成日） | 2026-10-06 |
| Last Updated（最終更新日） | 2026-10-06 |
| Owner（管理者） | Takashi Oikawa |
| Related Documents（関連文書） | [CONSTITUTION.md](./CONSTITUTION.md) / [AGENTS.md](./AGENTS.md) / [project-notes/CURRENT.md](./project-notes/CURRENT.md) / [CHANGELOG.md](./CHANGELOG.md) / [docs/design/README.md](./docs/design/README.md) |

> **Current Status（現在の状態）**
>
> 本Repositoryは設計段階である。実装は開始していない。
>
> 本READMEに記載した機能は、設計文書で定義した仕様であり、現時点で利用できる機能ではない。
>
> **設計レビュー中の訂正（2026-10-06）**：Userは記事URLを入力しない。本文・設計書に残る手入力フローはUserの申告と矛盾し、実装の根拠にしない。記事の取得・起動方法は未確認。
>
> 詳細な変更履歴は [CHANGELOG.md](./CHANGELOG.md) を参照する。

---

## Table of Contents（目次）

1. [Overview（概要）](#1-overview概要)
2. [Purpose（目的）](#2-purpose目的)
3. [Main Features（主な機能）](#3-main-features主な機能)
4. [Target Users（利用対象）](#4-target-users利用対象)
5. [Operating Environment（動作環境）](#5-operating-environment動作環境)
6. [Basic Usage Flow（基本的な利用フロー）](#6-basic-usage-flow基本的な利用フロー)
7. [Specification-Driven Development（SDDによる管理）](#7-specification-driven-developmentsddによる管理)
8. [Design Documents（設計書への入口）](#8-design-documents設計書への入口)
9. [Current Position（現在地点）](#9-current-position現在地点)

---

## 1. Overview（概要）

`jev-news-selector` は、PC上で利用者が選択した最新ニュース記事について、Jevが対面指導への有用度・対象レベル・記事カテゴリを判定し、その結果をMarkdownとしてObsidianへ保存するローカルBotである。

利用者はGoogleニュースを中心に記事を探し、選んだ記事のURLをターミナルからBotへ入力する。Botは最終的に到達した記事URLと記事の公開日を確認し、Bot実行日または前日（日本時間）に公開された記事だけを判定・保存する。

---

## 2. Purpose（目的）

IT初心者への対面指導で使うニュース記事の収集・判定・分類・蓄積を支援する。

- 利用者が選んだ記事について、指導で共有する価値を判定する
- 記事の対象レベルとカテゴリを分類する
- 判定結果をObsidianへ蓄積し、後から参照できるようにする

背景と目的の詳細は [01_REQUEST_DEFINITION.md](./docs/design/01_REQUEST_DEFINITION.md) を正とする。

---

## 3. Main Features（主な機能）

以下は設計上の機能であり、未実装である。

- ターミナルから記事URLを受け付ける
- 入力URLから、最終的に到達したニュース提供元の記事URL（最終記事URL）を取得する
- 記事のタイトル・公開日・判定に必要な本文を取得する
- 公開日を Asia/Tokyo（JST）の日付として扱い、Bot実行日または前日の記事だけを処理する。公開日を特定できない記事は処理しない
- Jevが指導有用度Score（0〜4）・対象レベル・記事カテゴリ（単一値）を判定する
- 判定結果を Obsidian Vault の `Bot News/YYYY-MM-DD/`（初回処理日）へ、1記事1Markdown（YAML frontmatter付き）として保存する
- 最終記事URLを一意キーとし、登録済みの記事は対象日条件を満たす場合にJevで再判定して既存Markdownを更新する
- 初期調整期間は人間評価を記録し、Jev判定と比較できるようにする。人間評価はJev再判定で上書きしない

機能要件の正本は [02_REQUIREMENTS_DEFINITION.md](./docs/design/02_REQUIREMENTS_DEFINITION.md) である。

---

## 4. Target Users（利用対象）

主利用者は Repository管理者本人である。不特定多数向けのサービスとして設計しない。

---

## 5. Operating Environment（動作環境）

| Item（項目） | Value（値） |
|---|---|
| Primary Environment（主環境） | MacBook Air M4 |
| OS | macOS |
| Execution（実行形態） | ローカル実行 |
| Language（言語） | Python |
| Input（入力） | ターミナル |

GUI、Webアプリ、クラウド常駐サービスとしては構成しない。Pythonライブラリ等の技術方式は未決であり、[05_ARCHITECTURE_DESIGN.md](./docs/design/05_ARCHITECTURE_DESIGN.md) で管理する。

---

## 6. Basic Usage Flow（基本的な利用フロー）

```text
Mac上でニュース閲覧
        ↓
Googleニュースを中心に記事を探す
＋必要に応じてその他サイト
        ↓
利用者が記事を選択
        ↓
記事URLをコピー
        ↓
ターミナルからBotへ入力
        ↓
最終記事URL取得
        ↓
記事公開日取得
        ↓
対象日判定（JST）
        ↓
記事タイトル・必要本文取得
        ↓
Jev判定
        ↓
Markdown生成（新規作成、または登録済み記事の更新）
        ↓
Obsidian Vault
        ↓
Bot News/YYYY-MM-DD/
```

操作と分岐の詳細は [04_UI_AND_FLOW_DESIGN.md](./docs/design/04_UI_AND_FLOW_DESIGN.md) を正とする。

---

## 7. Specification-Driven Development（SDDによる管理）

本Repositoryは SDD（Specification-Driven Development）で管理する。

- `docs/design/` の設計文書を正として実装を進める
- 設計文書が `Approved` になる前に実装を開始しない
- 確定仕様と未決事項を分離して管理する
- 作業規則は [CONSTITUTION.md](./CONSTITUTION.md) と [AGENTS.md](./AGENTS.md) に従う

Repository Purpose は `DEVELOPMENT` である。

---

## 8. Design Documents（設計書への入口）

設計文書の入口は [docs/design/README.md](./docs/design/README.md) である。

| File（ファイル名） | Role（役割） |
|---|---|
| [01_REQUEST_DEFINITION.md](./docs/design/01_REQUEST_DEFINITION.md) | なぜ作るか |
| [02_REQUIREMENTS_DEFINITION.md](./docs/design/02_REQUIREMENTS_DEFINITION.md) | 何を満たすか |
| [03_DATA_AND_SECURITY_DESIGN.md](./docs/design/03_DATA_AND_SECURITY_DESIGN.md) | データ・保存・セキュリティ |
| [04_UI_AND_FLOW_DESIGN.md](./docs/design/04_UI_AND_FLOW_DESIGN.md) | ターミナル操作と処理フロー |
| [05_ARCHITECTURE_DESIGN.md](./docs/design/05_ARCHITECTURE_DESIGN.md) | 構成と責務分離 |
| [06_OPERATION_AND_HANDOFF.md](./docs/design/06_OPERATION_AND_HANDOFF.md) | 運用と実装引き継ぎ |

---

## 9. Current Position（現在地点）

作業の現在地点、次の作業、阻害要因は [project-notes/CURRENT.md](./project-notes/CURRENT.md) を正とする。
