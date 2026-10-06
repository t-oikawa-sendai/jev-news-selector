# Design Documents Index（設計書一覧）




| Item（項目）                | Value（値）                                                                                                                                                                                       |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Document ID（文書ID）       | README-001                                                                                                                                                                                     |
| Version（バージョン）          | 0.1                                                                                                                                                                                            |
| Status（ステータス）           | Draft                                                                                                                                                                                          |
| Created Date（作成日）       | 2026-10-06                                                                                                                                                                                     |
| Last Updated（最終更新日）     | 2026-10-06                                                                                                                                                                                     |
| Owner（管理者）              | Takashi Oikawa                                                                                                                                                                                 |
| Related Documents（関連文書） | [README.md](../../README.md)（リポジトリルート） / [CHANGELOG.md](../../CHANGELOG.md)（リポジトリルート） / [CURRENT.md](../../project-notes/CURRENT.md) / solacom_main/docs/standards/DESIGN_DOCUMENT_STANDARD.md |


> 詳細な変更履歴はリポジトリルートの [CHANGELOG.md](../../CHANGELOG.md) を参照。

> **設計レビュー中の訂正（2026-10-06）**：Userは記事URLを入力しない。本文や関連設計書に残るUserによるURL手入力を前提とした記述は、この申告と矛盾するため、実装の根拠にしない。記事の取得・起動方法は未確認であり、確認前に方式を補完しない。

---

## Table of Contents（目次）

1. [Project Overview（プロジェクト・機能の概要）](#1-project-overviewプロジェクト機能の概要)
2. [Problem / Solution / Benefit Summary（問題・解決・効果の概要）](#2-problem-solution-benefit-summary問題解決効果の概要)
3. [Screen Overview（画面概要）](#3-screen-overview画面概要)
4. [Design Documents Index（設計書一覧）](#4-design-documents-index設計書一覧)
5. [Overall Design Policy（設計上の全体方針・前提）](#5-overall-design-policy設計上の全体方針前提)
6. [Glossary（用語集・略語定義）](#6-glossary用語集略語定義)
7. [Document Owners and Reviewers（文書管理者・レビュアー一覧）](#7-document-owners-and-reviewers文書管理者レビュアー一覧)

---

## 1. Project Overview（プロジェクト・機能の概要）

`jev-news-selector` は、PC上で利用者が選択した最新ニュース記事について、Jevが対面指導への有用度・対象レベル・記事カテゴリを判定し、その結果をMarkdownとしてObsidianへ保存するローカルBotである。主利用者は Repository管理者本人であり、IT初心者への対面指導で使う記事の収集・判定・分類・蓄積に用いる。

---

## 2. Problem / Solution / Benefit Summary（問題・解決・効果の概要）


| Item（項目）                    | Summary（概要）                                                                               | Detail Document（詳細文書）                                            |
| --------------------------- | ----------------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| Current Problems（現在の問題点）    | 対面指導で使う記事ごとに、指導有用度・対象レベル・カテゴリの判定と結果の蓄積を行う必要がある。公開日を確認できない記事は鮮度・信頼性を確認できない。                | [01_REQUEST_DEFINITION.md](./01_REQUEST_DEFINITION.md)           |
| Development Purpose（開発目的）   | 利用者が選んだ最新記事の判定・分類・蓄積を、ローカルBotで行えるようにする。                                                   | [01_REQUEST_DEFINITION.md](./01_REQUEST_DEFINITION.md)           |
| Solution Approach（解決方針） | UserによるURL手入力は行わない。記事の取得・起動方法は未確認であり、正しい方針の確認後に更新する。 | [01_REQUEST_DEFINITION.md](./01_REQUEST_DEFINITION.md) |
| System Functions（システム機能）    | URL入力、最終記事URL取得、JST基準の対象日判定、Jev判定、処理日フォルダへのMarkdown保存、最終記事URLによる一意管理と再判定更新、初期調整期間の人間評価記録。 | [02_REQUIREMENTS_DEFINITION.md](./02_REQUIREMENTS_DEFINITION.md) |
| Expected Benefits（期待効果）     | 判定結果が処理日単位で蓄積され、指導で使う記事を参照しやすくなる。人間評価との比較で判定基準を改善できる。                                     | [01_REQUEST_DEFINITION.md](./01_REQUEST_DEFINITION.md)           |
| Completion Criteria（完成判定基準） | 対象日条件を満たす記事だけが、Jev判定結果付きで1記事1Markdownとして重複なく保存・更新され、人間評価が保持されること。                         | [01_REQUEST_DEFINITION.md](./01_REQUEST_DEFINITION.md)           |


---

## 3. Screen Overview（画面概要）

本Botには GUI 画面がない。利用者の操作はターミナルからの記事URL入力のみである。

操作と処理フローの詳細: [04_UI_AND_FLOW_DESIGN.md](./04_UI_AND_FLOW_DESIGN.md)

---

## 4. Design Documents Index（設計書一覧）


| File（ファイル名）                                                        | Document Name（文書名）                        | Status（ステータス） | Version（バージョン） | Owner（担当者）     |
| ------------------------------------------------------------------ | ----------------------------------------- | ------------- | -------------- | -------------- |
| [01_REQUEST_DEFINITION.md](./01_REQUEST_DEFINITION.md)             | Request Definition（要求定義）                  | Draft         | 0.1            | Takashi Oikawa |
| [02_REQUIREMENTS_DEFINITION.md](./02_REQUIREMENTS_DEFINITION.md)   | Requirements Definition（要件定義）             | Draft         | 0.1            | Takashi Oikawa |
| [03_DATA_AND_SECURITY_DESIGN.md](./03_DATA_AND_SECURITY_DESIGN.md) | Data and Security Design（データ・セキュリティ設計）    | Draft         | 0.1            | Takashi Oikawa |
| [04_UI_AND_FLOW_DESIGN.md](./04_UI_AND_FLOW_DESIGN.md)             | UI and Flow Design（UI・フロー設計）              | Draft         | 0.1            | Takashi Oikawa |
| [05_ARCHITECTURE_DESIGN.md](./05_ARCHITECTURE_DESIGN.md)           | Architecture Design（アーキテクチャ設計）            | Draft         | 0.1            | Takashi Oikawa |
| [06_OPERATION_AND_HANDOFF.md](./06_OPERATION_AND_HANDOFF.md)       | Operation and Handoff Design（運用・詳細設計引き継ぎ） | Draft         | 0.1            | Takashi Oikawa |


---

## 5. Overall Design Policy（設計上の全体方針・前提）

### 5.1 Common Policy（共通方針）

- SDDで管理する。設計文書が `Approved` になる前に実装を開始しない
- 確定仕様と未決事項を分離する。未決事項は担当文書の Open Issues（未決事項）にのみ記載し、他文書からはIDで参照する
- 初期版の範囲を最小に保つ。将来必要になる可能性だけを理由に機能を追加しない
- 単一利用者（Repository管理者本人）がMacBook Air M4上でローカル実行する
- 日付の判定は Asia/Tokyo（JST）を基準とする
- 最終記事URLをシステム上の一意キーとする。入力URLは記事へ到達するための入力情報であり、一意キーではない
- Jevは記事の判定・分類だけを担当し、文章を生成しない
- Jev判定と人間評価は独立したデータとして扱い、互いに上書きしない
- 記事全文を保存しない。秘密情報をGitへ含めない

### 5.2 Open Issues Location（未決事項の所在）


| ID   | Open Issue（未決事項）   | Owner Document（管理文書）                                               |
| ---- | ------------------ | ------------------------------------------------------------------ |
| O-01 | 記事カテゴリ体系           | [02_REQUIREMENTS_DEFINITION.md](./02_REQUIREMENTS_DEFINITION.md)   |
| O-02 | 記事冒頭の保存量           | [03_DATA_AND_SECURITY_DESIGN.md](./03_DATA_AND_SECURITY_DESIGN.md) |
| O-03 | 人間評価入力方法           | [04_UI_AND_FLOW_DESIGN.md](./04_UI_AND_FLOW_DESIGN.md)             |
| O-04 | URL重複検索方式          | [05_ARCHITECTURE_DESIGN.md](./05_ARCHITECTURE_DESIGN.md)           |
| O-05 | 記事情報抽出方式           | [05_ARCHITECTURE_DESIGN.md](./05_ARCHITECTURE_DESIGN.md)           |
| O-06 | Obsidian Vault絶対パス | [03_DATA_AND_SECURITY_DESIGN.md](./03_DATA_AND_SECURITY_DESIGN.md) |


---

## 6. Glossary（用語集・略語定義）


| Term / Abbreviation（用語・略語） | Definition（定義）                                                                                           |
| -------------------------- | -------------------------------------------------------------------------------------------------------- |
| SDD                        | Specification-Driven Development。設計文書を正として実装を進める開発方式                                                     |
| Jev                        | 本Botで記事の指導有用度・対象レベル・記事カテゴリを判定する判定担当。呼出方式は [05_ARCHITECTURE_DESIGN.md](./05_ARCHITECTURE_DESIGN.md) で管理する |
| 入力URL                      | 利用者がGoogleニュース等からコピーしてBotへ入力したURL。記事へ到達するための入力情報                                                         |
| 最終記事URL（Final Article URL） | 入力URLから最終的に到達したニュース提供元の記事URL。システム上の一意キー                                                                  |
| 指導有用度Score                 | 記事を対面指導で共有する価値を示す0〜4の5段階の値                                                                               |
| 対象レベル                      | 記事が向く学習段階。`beginner` / `intermediate` / `other` の3値                                                      |
| 記事カテゴリ                     | 記事の主題による分類。1記事に1つ。対象レベルとは別の分類軸                                                                           |
| 実行日                        | Botを実行した日（JST）                                                                                           |
| 処理日（processed）             | Botが記事を初めて処理した日（JST）。保存先の日付フォルダ名に使い、再処理しても変えない                                                           |
| 公開日（published）             | 記事自体の公開日。JSTの日付として扱う                                                                                     |
| 対象日判定                      | 公開日がBot実行日または前日であるかを判定する処理                                                                               |
| 再処理                        | 登録済みの最終記事URLが再入力され、対象日条件を満たす場合に、記事情報を再取得してJevで再判定し、既存Markdownを更新する処理                                     |
| YAML frontmatter           | 記事Markdown先頭の、判定・管理用データを保存する領域                                                                           |
| 初期調整期間                     | Jev判定と人間評価を比較し、判定基準を調整する期間。終了は利用者が判断する                                                                   |
| 人間評価                       | 初期調整期間に利用者が記録する `human_decision` と `human_score`                                                         |
| 自動選別条件                     | Jev判定結果等による記事の自動選別の条件。未決であり、初期版では使用しない                                                                   |
| 記事冒頭                       | 記事本文の先頭部分。保存量は未決（O-02）                                                                                   |
| Bot News                   | Obsidian Vault 内の保存先フォルダ名                                                                                |


---

## 7. Document Owners and Reviewers（文書管理者・レビュアー一覧）


| Role（役割）              | Name（氏名）                  | Assigned Documents（担当文書） |
| --------------------- | ------------------------- | ------------------------ |
| Document Owner（文書管理者） | Takashi Oikawa            | All Documents（全文書）       |
| Reviewer（レビュアー）       | Takashi Oikawa（利用者）/ 設計担当 | All Documents（全文書）       |
