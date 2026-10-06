# Request Definition（要求定義）

<!-- Document Info（文書情報） -->
| Item（項目） | Value（値） |
|---|---|
| Document ID（文書ID） | REQ-001 |
| Version（バージョン） | 0.1 |
| Status（ステータス） | Draft |
| Created Date（作成日） | 2026-10-06 |
| Last Updated（最終更新日） | 2026-10-06 |
| Owner（管理者） | Takashi Oikawa |
| Related Documents（関連文書） | README.md / 02_REQUIREMENTS_DEFINITION.md / 06_OPERATION_AND_HANDOFF.md |

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

本文書は、`jev-news-selector` を作る理由を定義する正本である。背景・問題・目的・利用者・対象範囲・対象外・期待効果・制約・完成条件を定め、要件定義以降の前提とする。

読者は、利用者・設計担当・実装担当である。

---

## 2. Scope（対象範囲）

- 利用者が選択したニュース記事のURLを、ターミナルからBotへ入力してから、判定結果をObsidianへ保存するまでの初期版Bot全体
- 初期調整期間における人間評価の位置付け

---

## 3. Out of Scope（対象外範囲）

以下は初期版の対象外とする。本節を初期版対象外の正本とする。

| Item（項目） | Description（内容） |
|---|---|
| Input Channels（入力経路） | LINE Bot、Webフォーム、GUI、ブラウザ拡張によるURL入力 |
| External Storage（外部保存先） | Notion、Pocket |
| Automatic Collection（自動収集） | ニュース自動巡回、ニュース自動検索、ニュース全自動収集 |
| Automatic Discard（自動破棄） | Jev Score 等による記事の自動破棄・自動選別 |
| Human Evaluation GUI（人間評価GUI） | 人間評価専用GUI |
| Model Retraining（モデル再学習） | Jevモデルそのものの再学習 |
| Deployment Form（提供形態） | Webアプリ化、クラウド常駐化 |
| Text Generation（文章生成） | Jevによる記事全文の書き換え、授業用文章の生成 |

将来必要になる可能性だけを理由に、上記を初期版へ追加しない。

自動選別は、蓄積した評価データの分析後に利用者が条件を承認し、設計書を更新した後にのみ導入できる。手順は [06_OPERATION_AND_HANDOFF.md](./06_OPERATION_AND_HANDOFF.md) §5.6 を正とする。

---

## 4. Assumptions（前提条件）

- 利用者は MacBook Air M4（macOS）上でニュースを閲覧し、記事を自ら一次選択する
- 記事の入口は Googleニュースを中心とし、必要に応じてその他サイトを利用する
- Obsidian Vault は利用者のMac上に存在する。絶対パスは未決である（O-06。[03_DATA_AND_SECURITY_DESIGN.md](./03_DATA_AND_SECURITY_DESIGN.md) 参照）
- Jevを利用して記事を判定できる。呼出方式は [05_ARCHITECTURE_DESIGN.md](./05_ARCHITECTURE_DESIGN.md) で管理する

---

## 5. Definition Details（定義内容）

### 5.1 Background and Purpose（背景・課題・目的）

#### Background（背景）

Repository管理者は、IT初心者への対面指導を行っている。指導で共有するニュース記事は、利用者自身が選んでいる。

#### Problems（問題）

- 対面指導で使うニュース記事について、指導有用度・対象レベル・記事カテゴリの判定と分類、および結果の蓄積を、利用者が選んだ記事ごとに行う必要がある
- 公開日を確認できない記事は、ニュースとしての鮮度・信頼性を確認できない

#### Purpose（目的）

利用者が選択した最新ニュース記事について、Jevが指導有用度・対象レベル・記事カテゴリを判定し、その結果をMarkdownとしてObsidianへ保存する。これにより、対面指導で使うニュース記事の収集・判定・分類・蓄積を支援する。

#### Expected Benefits（期待効果）

- 選んだ記事の判定・分類・蓄積をBotで行える
- 判定結果が処理日単位でObsidianに蓄積され、指導で使う記事を参照しやすくなる
- 公開日を基準に対象を絞るため、鮮度を確認できない記事が蓄積に混入しない
- 初期調整期間の人間評価との比較により、Jevへの instructions と criteria を改善できる

### 5.2 Stakeholders（ステークホルダー一覧と関心事）

| Stakeholder（ステークホルダー） | Interests and Requests（関心事・要求） |
|---|---|
| Repository管理者（主利用者） | 選んだ記事の有用度・対象レベル・カテゴリを判定し、Obsidianへ蓄積したい |
| 対面指導を受けるIT初心者（間接受益者） | 指導で記事を共有される。システムを直接操作しない |

不特定多数の利用者は想定しない。

### 5.3 User Stories and Use Cases（ユーザーストーリー・ユースケース概要）

| ID | User Story / Use Case（ユーザーストーリー / ユースケース） |
|---|---|
| US-001 | 利用者として、選んだ記事のURLをターミナルから入力し、判定結果をObsidianへ保存したい |
| US-002 | 利用者として、Bot実行日または前日に公開された記事だけを処理し、公開日を特定できない記事や古い記事を除外したい |
| US-003 | 利用者として、記事ごとに指導有用度・対象レベル・記事カテゴリを判定させたい |
| US-004 | 利用者として、Googleニュース等のどのURLから入力しても、同じ記事を重複保存せず1記事1ファイルで蓄積したい |
| US-005 | 利用者として、対象期間内に同じ記事を再入力した場合は、最新の記事情報とJev判定で既存Markdownを更新したい |
| US-006 | 利用者として、初期調整期間にJev判定と自分の評価を並べて記録し、差を確認したい。記録した評価はJev再判定で失われないようにしたい |
| US-007 | 利用者として、Jev判定が安定したと自分で判断した後は、新しい記事への人間評価入力をやめたい。記録済みの人間評価は残したい |

機能要件への対応は [02_REQUIREMENTS_DEFINITION.md](./02_REQUIREMENTS_DEFINITION.md) §5.6 を正とする。

### 5.4 Constraints（制約条件）

| Type（種別） | Constraint（制約内容） |
|---|---|
| Budget（予算） | 指定なし |
| Deadline（期限） | 指定なし |
| Technical（技術） | MacBook Air M4 / macOS 上でのローカル実行。言語は Python。入力はターミナル。GUI・Webアプリ・クラウド常駐サービスとして構成しない |
| Regulatory（法規） | 本文書で追加する法規上の制約はない |
| Data（データ） | 記事全文を保存しない。APIキー等の秘密情報をGit・設計書・READMEに含めない |
| Users（利用者） | 主利用者は Repository管理者本人のみ |

### 5.5 Success Criteria and Acceptance Conditions（成功基準・受け入れ条件）

| ID | Success Criteria / Acceptance Condition（成功基準・受け入れ条件） |
|---|---|
| SC-001 | ターミナルから記事URLを入力すると、対象日条件を満たす記事について、Jev判定結果を含むMarkdownが `Bot News/<処理日>/` に保存される |
| SC-002 | 公開日（JST）がBot実行日・前日のいずれでもない記事、および公開日を特定できない記事は、新規保存も既存Markdownの更新もされない |
| SC-003 | 入力URLが異なっても最終記事URLが同じ記事は、同一記事として扱われる |
| SC-004 | 登録済みの最終記事URLを対象日条件内で再入力すると、新しいファイルは作られず、初回処理日フォルダの既存Markdownが再判定結果で更新され、`processed` は初回処理日のまま保持される |
| SC-005 | 同一処理日フォルダで同じタイトル・別の最終記事URLの記事を保存しても、既存ファイルが上書きされない |
| SC-006 | 記録済みの人間評価が、Jev再判定の後も保持される |
| SC-007 | 記事全文と秘密情報が、保存したMarkdownおよびGitに含まれない |

テスト工程での検証基準は [06_OPERATION_AND_HANDOFF.md](./06_OPERATION_AND_HANDOFF.md) §5.3 に記載する。

---

## 6. Open Issues（未決事項）

本文書で管理する未決事項はない。

未決事項 O-01〜O-06 は担当文書で管理する。所在は [README.md](./README.md) §5.2 を参照する。

---

## 7. Handoff to Detail Design（詳細設計への引き継ぎ）

- Jevの役割は判定・分類に限る。文章生成の要求はない
- 対象日判定を通過した記事を全件保存するのは、初期調整期間にJev判定と人間評価を比較するためである。自動選別条件が正式に決まるまで全件保存を続ける
- 人間評価は恒久運用ではない。Jev判定が安定したと利用者が判断した時点で、新しい記事への日常入力を終了する
- 機能要件は [02_REQUIREMENTS_DEFINITION.md](./02_REQUIREMENTS_DEFINITION.md) を正とする
