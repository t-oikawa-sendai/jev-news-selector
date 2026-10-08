# Design Documents Index（設計書一覧）

<!-- Document Info（文書情報） -->
| Item（項目） | Value（値） |
|---|---|
| Document ID（文書ID） | README-001 |
| Version（バージョン） | 0.1 |
| Status（ステータス） | Draft |
| Created Date（作成日） | 2026-10-06 |
| Last Updated（最終更新日） | 2026-10-08 |
| Owner（管理者） | Takashi Oikawa |
| Related Documents（関連文書） | [README.md](../../README.md)（リポジトリルート） / [CHANGELOG.md](../../CHANGELOG.md)（リポジトリルート） / [CURRENT.md](../../project-notes/CURRENT.md) / solacom_main/docs/standards/DESIGN_DOCUMENT_STANDARD.md |

> 詳細な変更履歴はリポジトリルートの [CHANGELOG.md](../../CHANGELOG.md) を参照。

> 本設計は未承認の Draft である。撤回事項・ID未登録の未確認事項・現在地点は [CURRENT.md](../../project-notes/CURRENT.md) を正とする。

---

## Table of Contents（目次）

1. [Project Overview（プロジェクト・機能の概要）](#1-project-overviewプロジェクト機能の概要)
2. [Problem / Solution / Benefit Summary（問題・解決・効果の概要）](#2-problem--solution--benefit-summary問題解決効果の概要)
3. [Screen Overview（画面概要）](#3-screen-overview画面概要)
4. [Design Documents Index（設計書一覧）](#4-design-documents-index設計書一覧)
5. [Overall Design Policy（設計上の全体方針・前提）](#5-overall-design-policy設計上の全体方針前提)
6. [Glossary（用語集・略語定義）](#6-glossary用語集略語定義)
7. [Document Owners and Reviewers（文書管理者・レビュアー一覧）](#7-document-owners-and-reviewers文書管理者レビュアー一覧)

---

## 1. Project Overview（プロジェクト・機能の概要）

`jev-news-selector` は、Userが任意の時刻に手動起動するローカルBotである。Botは GoogleニュースのRSSで記事を取得する。この方式は採用済みであり、検証は未完了である。入口は分野・検索語で絞り、検証用の件数上限を併用する。正本は [02_REQUIREMENTS_DEFINITION.md](./02_REQUIREMENTS_DEFINITION.md) §5.1.6 である。具体的な分野・検索語は暫定採用済みであり、具体一覧は原記録未復元のため本書で補完しない。Jevが対面指導への有用度・対象レベル・記事カテゴリを判定し、その結果をMarkdownとしてObsidianへ保存する。主Userは Repository管理者本人であり、IT初心者への対面指導で使う記事の収集・判定・分類・蓄積に用いる。

---

## 2. Problem / Solution / Benefit Summary（問題・解決・効果の概要）

| Item（項目） | Summary（概要） | Detail Document（詳細文書） |
|---|---|---|
| Current Problems（現在の問題点） | 対面指導で使う記事ごとに、指導有用度・対象レベル・カテゴリの判定と結果の蓄積を行う必要がある。公開日を確認できない記事は鮮度・信頼性を確認できない。 | [01_REQUEST_DEFINITION.md](./01_REQUEST_DEFINITION.md) |
| Development Purpose（開発目的） | 最新ニュース記事の判定・分類・蓄積を、ローカルBotで行えるようにする。 | [01_REQUEST_DEFINITION.md](./01_REQUEST_DEFINITION.md) |
| Solution Approach（解決方針） | Userが任意の時刻にBotを手動起動する。Botは GoogleニュースのRSSで、分野・検索語と検証用件数上限により絞った記事を取得し、JST基準の対象日判定を通過した記事をJevで判定してObsidianへ保存・更新する。入口の正本は [02_REQUIREMENTS_DEFINITION.md](./02_REQUIREMENTS_DEFINITION.md) §5.1.6。 | [01_REQUEST_DEFINITION.md](./01_REQUEST_DEFINITION.md) |
| System Functions（システム機能） | 任意時刻の手動起動、GoogleニュースRSSによる記事取得（検証は未完了）、分野・検索語と検証用件数上限による入口、最終記事URL取得、JST基準の対象日判定、Jev判定（Scoreは返された値のまま保存）、入口を通過し対象日条件を満たした記事の全件保存、処理日フォルダへのMarkdown保存、最終記事URLによる一意管理と再判定更新（`published` は対象条件を満たした最新の取得値へ更新）、初期調整期間のUser評価記録。 | [02_REQUIREMENTS_DEFINITION.md](./02_REQUIREMENTS_DEFINITION.md) |
| Expected Benefits（期待効果） | 判定結果が処理日単位で蓄積され、指導で使う記事を参照しやすくなる。User評価との比較で判定基準を改善できる。 | [01_REQUEST_DEFINITION.md](./01_REQUEST_DEFINITION.md) |
| Completion Criteria（完成判定基準） | 対象日条件を満たす記事だけが、Jev判定結果付きで1記事1Markdownとして重複なく保存・更新され、User評価が保持されること。 | [01_REQUEST_DEFINITION.md](./01_REQUEST_DEFINITION.md) |

---

## 3. Screen Overview（画面概要）

本設計では有効な画面を定義しない。起動のUI・コマンド形式は未確認である。

Userの操作は次の2つである。

- 任意の時刻にBotを手動起動する（URL入力を伴わない）
- 初期調整期間にUser評価（`human_decision` / `human_score`）を記録する。入力方法は O-03

操作と処理フローの詳細: [04_UI_AND_FLOW_DESIGN.md](./04_UI_AND_FLOW_DESIGN.md)

図は次を開く。詳細図の正本は04と05であり、本書では繰り返さない。

- [入口の図](./04_UI_AND_FLOW_DESIGN.md#entry-diagram)
- [記事ごとの図](./04_UI_AND_FLOW_DESIGN.md#article-diagram)
- [構成の図](./05_ARCHITECTURE_DESIGN.md#system-diagram)
- [データの流れ](./05_ARCHITECTURE_DESIGN.md#data-flow-diagram)

---

## 4. Design Documents Index（設計書一覧）

| File（ファイル名） | Document Name（文書名） | Status（ステータス） | Version（バージョン） | Owner（担当者） |
|---|---|---|---|---|
| [01_REQUEST_DEFINITION.md](./01_REQUEST_DEFINITION.md) | Request Definition（要求定義） | Draft | 0.1 | Takashi Oikawa |
| [02_REQUIREMENTS_DEFINITION.md](./02_REQUIREMENTS_DEFINITION.md) | Requirements Definition（要件定義） | Draft | 0.1 | Takashi Oikawa |
| [03_DATA_AND_SECURITY_DESIGN.md](./03_DATA_AND_SECURITY_DESIGN.md) | Data and Security Design（データ・セキュリティ設計） | Draft | 0.1 | Takashi Oikawa |
| [04_UI_AND_FLOW_DESIGN.md](./04_UI_AND_FLOW_DESIGN.md) | UI and Flow Design（UI・フロー設計） | Draft | 0.1 | Takashi Oikawa |
| [05_ARCHITECTURE_DESIGN.md](./05_ARCHITECTURE_DESIGN.md) | Architecture Design（アーキテクチャ設計） | Draft | 0.1 | Takashi Oikawa |
| [06_OPERATION_AND_HANDOFF.md](./06_OPERATION_AND_HANDOFF.md) | Operation and Handoff Design（運用・詳細設計引き継ぎ） | Draft | 0.1 | Takashi Oikawa |

---

## 5. Overall Design Policy（設計上の全体方針・前提）

### 5.1 Common Policy（共通方針）

- SDDで管理する。設計文書が `Approved` になる前に実装を開始しない
- 確定仕様と未決事項を分離する。未決事項は担当文書の Open Issues（未決事項）にのみ記載し、他文書からはIDで参照する。ID未登録の未確認事項は [CURRENT.md](../../project-notes/CURRENT.md) の Blockers を参照する
- 初期版の範囲を最小に保つ。将来必要になる可能性だけを理由に機能を追加しない
- 単一User（Repository管理者本人）がMacBook Air M4上でローカル実行する。起動は任意時刻の手動起動とし、定期自動起動は採用しない
- Userによる記事の探索・選択・URLコピー・URL入力を前提にしない
- 日付の判定は Asia/Tokyo（JST）を基準とする
- 最終記事URLをシステム上の一意キーとする。記事取得で得たURLが最終記事URLと異なる場合、そのURLは一意キーではない
- Jevは記事の判定・分類だけを担当し、文章を生成しない
- Jev判定とUser評価は独立したデータとして扱い、互いに上書きしない
- 記事全文を保存しない。秘密情報をGitへ含めない

### 5.2 Open Issues Location（未決事項の所在）

| ID | Open Issue（未決事項） | Owner Document（管理文書） |
|---|---|---|
| O-01 | 記事カテゴリ体系 | [02_REQUIREMENTS_DEFINITION.md](./02_REQUIREMENTS_DEFINITION.md) |
| O-02 | 記事冒頭の保存量 | [03_DATA_AND_SECURITY_DESIGN.md](./03_DATA_AND_SECURITY_DESIGN.md) |
| O-03 | User評価入力方法 | [04_UI_AND_FLOW_DESIGN.md](./04_UI_AND_FLOW_DESIGN.md) |
| O-04 | URL重複検索方式 | [05_ARCHITECTURE_DESIGN.md](./05_ARCHITECTURE_DESIGN.md) |
| O-05 | 記事情報抽出方式 | [05_ARCHITECTURE_DESIGN.md](./05_ARCHITECTURE_DESIGN.md) |
| O-06 | Obsidian Vault絶対パス | [03_DATA_AND_SECURITY_DESIGN.md](./03_DATA_AND_SECURITY_DESIGN.md) |

O-01〜O-06 に該当しない未確認事項（RSSのURL・使用ライブラリ、起動のUI・コマンド形式、再処理時のファイル名、ファイル名に使えない文字の扱い、処理失敗時の扱い、データベースの採否）は ID未登録であり、[CURRENT.md](../../project-notes/CURRENT.md) の Blockers に記録する。

入口の分野・検索語は暫定採用済みである。管理は [02_REQUIREMENTS_DEFINITION.md](./02_REQUIREMENTS_DEFINITION.md) §5.1.6 であり、[06_OPERATION_AND_HANDOFF.md](./06_OPERATION_AND_HANDOFF.md) からも参照する。具体一覧は原記録未復元のため、本書で補完しない。保存後の `jev_category` の候補とは別である。

O-05 の状態は OPEN のままとする。Userから記事情報抽出方式の暫定採用を指摘する発言がある。タイトル取得方式・公開日取得方式・本文取得方式・使用ライブラリの具体値は原記録未復元である。再選定が必要とは断定しない。

---

## 6. Glossary（用語集・略語定義）

| Term / Abbreviation（用語・略語） | Definition（定義） |
|---|---|
| SDD | Specification-Driven Development。設計文書を正として実装を進める開発方式 |
| Jev | 本Botで記事の指導有用度・対象レベル・記事カテゴリを判定する判定担当。呼出方式は [05_ARCHITECTURE_DESIGN.md](./05_ARCHITECTURE_DESIGN.md) で管理する |
| 手動起動 | Userが任意の時刻にBotを起動すること。記事の探索・選択・URLコピー・URL手入力を伴わない。起動のUI・コマンド形式は未確認 |
| 入口 | 分野・検索語による絞り込みと、検証用件数上限の併用。正本は [02_REQUIREMENTS_DEFINITION.md](./02_REQUIREMENTS_DEFINITION.md) §5.1.6。具体的な分野・検索語は暫定採用済みであり、具体一覧は原記録未復元 |
| 検証用件数上限 | 全検索語の合計で1回最大50件。検証用の上限であり、通常運用の上限へ自動適用しない。超過分はその回では無視する |
| 最終記事URL（Final Article URL） | 処理対象記事について、最終的に到達したニュース提供元の記事URL。システム上の一意キー |
| 指導有用度Score | 記事を対面指導で共有する価値を示す値。評価基準は0〜4の5段階。`jev_score` にはJevが返した値（小数を含む）をそのまま保存する |
| 対象レベル | 記事が向く学習段階。`beginner` / `intermediate` / `other` の3値 |
| 記事カテゴリ | 記事の主題による分類。1記事に1つ。対象レベルとは別の分類軸 |
| 実行日 | Botを実行した日（JST） |
| 処理日（processed） | Botが記事を初めて処理した日（JST）。保存先の日付フォルダ名に使い、再処理しても変えない |
| 公開日（published） | 記事自体の公開日。JSTの日付として扱う。再処理時は最新の取得値へ更新する |
| 対象日判定 | 公開日がBot実行日または前日であるかを判定する処理 |
| 再処理 | 登録済みの最終記事URLの記事が再び処理対象となり、対象日条件を満たす場合に、記事情報を再取得してJevで再判定し、既存Markdownを更新する処理 |
| YAML frontmatter | 記事Markdown先頭の、判定・管理用データを保存する領域 |
| 初期調整期間 | Jev判定とUser評価を比較し、判定基準を調整する期間。終了はUserが判断する |
| User評価 | 初期調整期間にUserが記録する `human_decision` と `human_score` |
| 自動選別条件 | Jev判定結果等による記事の自動選別の条件。未決であり、初期版では使用しない |
| 記事冒頭 | 記事本文の先頭部分。保存量は未決（O-02） |
| Bot News | Obsidian Vault 内の保存先フォルダ名 |

---

## 7. Document Owners and Reviewers（文書管理者・レビュアー一覧）

| Role（役割） | Name（氏名） | Assigned Documents（担当文書） |
|---|---|---|
| Document Owner（文書管理者） | Takashi Oikawa | All Documents（全文書） |
| Reviewer（レビュアー） | Takashi Oikawa（User）/ 設計担当 | All Documents（全文書） |
