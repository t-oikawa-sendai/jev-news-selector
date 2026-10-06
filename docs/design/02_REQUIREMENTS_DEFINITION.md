# Requirements Definition（要件定義）

<!-- Document Info（文書情報） -->
| Item（項目） | Value（値） |
|---|---|
| Document ID（文書ID） | REQS-001 |
| Version（バージョン） | 0.1 |
| Status（ステータス） | Draft |
| Created Date（作成日） | 2026-10-06 |
| Last Updated（最終更新日） | 2026-10-06 |
| Owner（管理者） | Takashi Oikawa |
| Related Documents（関連文書） | README.md / 01_REQUEST_DEFINITION.md / 03_DATA_AND_SECURITY_DESIGN.md / 04_UI_AND_FLOW_DESIGN.md / 05_ARCHITECTURE_DESIGN.md / 06_OPERATION_AND_HANDOFF.md |

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

本文書は、`jev-news-selector` が満たすべき機能要件・非機能要件を定義する正本である。データ・UI・アーキテクチャ・運用の各設計書の基準とする。

読者は、利用者・設計担当・実装担当である。

---

## 2. Scope（対象範囲）

- 記事URLの入力から Obsidian への保存・更新までの初期版機能要件
- 公開日の扱いと対象日判定の規則
- Jev判定（指導有用度Score・対象レベル・記事カテゴリ）の値域
- 登録済み記事の再処理
- 初期調整期間の人間評価に関する要件
- 初期版の非機能要件

---

## 3. Out of Scope（対象外範囲）

初期版の対象外は [01_REQUEST_DEFINITION.md](./01_REQUEST_DEFINITION.md) §3 を正とする。本文書では再掲しない。

自動選別条件は未決であり、本文書の要件に含めない。

---

## 4. Assumptions（前提条件）

- 記事は利用者が一次選択する。Botは記事を探さない
- 日付の判定は Asia/Tokyo（JST）を基準とする
- 記事カテゴリの10分類は仮定であり、最終確定ではない（O-01）

---

## 5. Definition Details（定義内容）

### 5.1 Functional Requirements（機能要件一覧）

いずれも初期版の成立に必要な機能である。未決事項・将来機能・初期版対象外は含めない。

| ID | Feature Name（機能名） | Priority（優先度） | Details（詳細） |
|---|---|---|---|
| FR-001 | URL Input（URL入力） | High | 利用者がGoogleニュース等からコピーした記事URLを、ターミナルから入力として受け付ける |
| FR-002 | Final Article URL Retrieval（最終記事URL取得） | High | 入力URLから、最終的に到達したニュース提供元の記事URL（最終記事URL）を取得する。入力URLは記事へ到達するための入力情報として扱う |
| FR-003 | Article Information Retrieval（記事情報取得） | High | 記事タイトル・記事公開日・Jev判定と記事冒頭の保存に必要な本文を取得する。抽出方式は O-05（[05_ARCHITECTURE_DESIGN.md](./05_ARCHITECTURE_DESIGN.md)） |
| FR-004 | Publication Date Determination（公開日の決定） | High | §5.1.4 の規則で、記事公開日を JST の日付として決定する |
| FR-005 | Unidentifiable Publication Date（公開日を特定できない記事） | High | 公開日を取得できない、特定できない、または推測しなければ日付を決められない記事は処理対象外とする。Bot実行日・取得日・更新日・推測値などで補完しない |
| FR-006 | Target Date Judgment（対象日判定） | High | 記事公開日が Bot実行日または Bot実行日の前日（いずれも JST）である場合のみ処理対象とする。登録済みの記事でも毎回判定する |
| FR-007 | Out-of-Target Handling（対象外記事の扱い） | High | FR-005 または FR-006 で対象外となった記事は、Jev判定・新規保存・既存Markdownの更新を行わない |
| FR-008 | Jev Judgment（Jev判定） | High | 対象日判定を通過した記事について、Jevが指導有用度Score・対象レベル・記事カテゴリを判定する。Jevに記事全文の書き換えや授業用文章の生成をさせない |
| FR-009 | Teaching Usefulness Score（指導有用度Score） | High | 0〜4の5段階とする。定義は §5.1.1 |
| FR-010 | Target Level（対象レベル） | High | `beginner` / `intermediate` / `other` の3値とする。定義は §5.1.2 |
| FR-011 | Article Category（記事カテゴリ） | High | 1記事につき単一値とする。§5.1.3 の候補から Jev が1つを選択する。候補の分類体系は仮定である（O-01） |
| FR-012 | Save All Target Articles（対象記事の全件保存） | High | 対象日判定を通過した記事は全件保存する。Jev Score を理由に自動破棄しない。Score 0 の記事も保存する。自動選別条件が利用者に承認され設計書へ反映されるまで、全件保存を継続する |
| FR-013 | Markdown Storage（Markdown保存） | High | 1記事を1つのMarkdownファイルとして、Obsidian Vault の `Bot News/YYYY-MM-DD/` へ保存する。日付は記事公開日ではなく初回のBot処理日とする。判定・管理用データは YAML frontmatter に保存する。詳細は [03_DATA_AND_SECURITY_DESIGN.md](./03_DATA_AND_SECURITY_DESIGN.md) |
| FR-014 | URL Uniqueness（URL一意性） | High | 最終記事URLをシステム上の一意キーとする。入力URLは一意キーにしない。未登録の最終記事URLは新規Markdownを作成する。登録済みの最終記事URLは新しいファイルを作成せず、既存Markdownを更新する。別の日に入力しても、新しい処理日フォルダへ移動・複製しない |
| FR-015 | Reprocessing of Registered Article（登録済み記事の再処理） | High | 登録済みの最終記事URLが入力され、対象日判定を通過した場合は、記事情報を再取得し、Jevで再判定し、既存Markdownを更新する。更新項目と保持項目は §5.1.5 |
| FR-016 | Same Title with Different URL（同一タイトル・別URL） | High | 同一処理日フォルダ内に同じファイル名があり、最終記事URLが異なる場合は、別記事として別ファイルへ保存する。同じタイトルであることを理由に既存記事を上書きしない。命名規則は [03_DATA_AND_SECURITY_DESIGN.md](./03_DATA_AND_SECURITY_DESIGN.md) |
| FR-017 | Human Evaluation（人間評価） | High | 初期調整期間のみ、記事ごとに `human_decision`（`adopted` / `rejected`）と `human_score`（0〜4）を記録できる。`human_score` の段階定義は §5.1.1 と同じとする。入力方法は O-03（[04_UI_AND_FLOW_DESIGN.md](./04_UI_AND_FLOW_DESIGN.md)） |
| FR-018 | Separation of Jev and Human Evaluation（Jev評価と人間評価の分離） | High | Jev判定と人間評価を独立したデータとして保持する。Jev判定を人間評価で上書きしない。Jev再判定で人間評価を削除・初期化・上書きしない |
| FR-019 | Processing without Human Evaluation（人間評価なしでの処理） | High | 人間評価が記録されていない記事でも、Jev判定と保存は成立する。人間評価の日常入力を終了した後も、対象日判定を通過した記事の全件保存を継続する |
| FR-020 | Retention of Recorded Human Evaluation（記録済み人間評価の保持） | High | 人間評価の日常入力を終了した後も、記録済みの `human_decision` / `human_score` を削除しない。過去データを一括削除しない |

#### 5.1.1 Teaching Usefulness Score Definition（指導有用度Score定義）

本定義を変更しない。

| Score | Definition（定義） |
|---:|---|
| 0 | 対面指導で使う価値がほぼない |
| 1 | 関連はあるが、共有する価値は低い |
| 2 | 生徒によっては参考になる |
| 3 | 対面指導で共有する価値が高い |
| 4 | 特に有益で、積極的に共有したい |

#### 5.1.2 Target Level Definition（対象レベル定義）

| Value（値） | Definition（定義） |
|---|---|
| `beginner` | IT初心者向け |
| `intermediate` | 実践・応用寄り |
| `other` | 上記に分類しにくいもの |

対象レベルと記事カテゴリを同じ分類軸にしない。

#### 5.1.3 Article Category（記事カテゴリ）

現在は以下の10分類を候補として仮定する。最終確定ではない（O-01）。

```text
AI
Java
Python
DB
Git-GitHub
就職
業界動向
セキュリティ
マインドセット
その他
```

- `jev_category` は単一値とする。複数カテゴリの配列にしない
- Jev が候補から1つを選択する
- AI判断でカテゴリを追加・削除・統合・分割・改名しない

#### 5.1.4 Publication Date Rules（公開日の規則）

| Source Information（記事側の情報） | Publication Date（公開日の扱い） |
|---|---|
| タイムゾーン情報を含む公開日時 | Asia/Tokyo へ変換し、変換後の日付を公開日とする |
| 時刻・タイムゾーンがなく、日付だけが明示されている | 明示された日付を公開日とする。タイムゾーンを推測で補完しない |
| 取得できない、特定できない、推測しなければ日付を決められない | 処理対象外（FR-005） |

例:

```text
Source: 2026-10-05 23:30 UTC
JST:    2026-10-06 08:30 JST
公開日: 2026-10-06
```

対象日判定の例（Bot実行日 2026-10-06 JST）:

| Publication Date（公開日） | Result（判定） |
|---|---|
| 2026-10-06 | 対象 |
| 2026-10-05 | 対象 |
| 2026-10-04 | 対象外 |
| それ以前 | 対象外 |

#### 5.1.5 Reprocessing Update Rules（再処理時の更新規則）

| Item（項目） | Behavior（再処理時の扱い） |
|---|---|
| 記事タイトル | 最新の取得結果へ更新する |
| 記事冒頭 | 最新の取得結果へ更新する |
| `jev_score` | 最新の判定結果へ更新する |
| `jev_audience` | 最新の判定結果へ更新する |
| `jev_category` | 最新の判定結果へ更新する |
| `processed` | 初回処理日を保持する。更新日の意味へ変更しない |
| `human_decision` / `human_score` | 保持する。削除・初期化・上書きしない |
| 保存先フォルダ | 初回処理日フォルダのまま。新しい日付フォルダへ移動・複製しない |

- 公開日も記事から再取得し、対象日判定に使う。信頼できる公開日を取得できない場合は更新処理を行わない
- 例: `jev_score: 2` / `human_decision: adopted` / `human_score: 4` の記事が再判定で `jev_score: 4` になっても、`human_decision: adopted` / `human_score: 4` は保持する

### 5.2 Non-Functional Requirements（非機能要件）

| Type（種別） | Requirement（要件内容） |
|---|---|
| Performance（性能） | 指定なし |
| Availability（可用性） | 利用者がターミナルから起動したときに動作する。常駐・24時間稼働は要求しない |
| Security Requirement Level（セキュリティ要求レベル） | APIキー等の秘密情報を Git・設計書・README に含めない。記事全文を保存しない。設計仕様は [03_DATA_AND_SECURITY_DESIGN.md](./03_DATA_AND_SECURITY_DESIGN.md) |
| Maintainability（保守性） | 初期調整期間の比較結果を基に、Jevへの instructions と criteria を改善できること。責務分離は [05_ARCHITECTURE_DESIGN.md](./05_ARCHITECTURE_DESIGN.md) |
| Other（その他） | タイムゾーンは Asia/Tokyo（JST）とする |

### 5.3 Screen List（画面一覧）

本Botには GUI 画面がない。利用者との接点はターミナルのみである。

| Screen ID（画面ID） | Screen Name（画面名） | Purpose / Overview（利用目的・概要） |
|---|---|---|
| SCR-001 | Terminal（ターミナル） | 記事URLの入力と処理結果の表示 |

詳細は [04_UI_AND_FLOW_DESIGN.md](./04_UI_AND_FLOW_DESIGN.md) に記載する。

### 5.4 API Overview（API一覧の概要）

本Botは外部へAPIを公開しない。本Botが利用する外部連携は次のとおりである。

| API ID | API Name / Endpoint Overview（API名 / エンドポイント概要） | Purpose（用途） |
|---|---|---|
| API-001 | Article Retrieval（記事情報取得） | 入力URLから最終記事URLへ到達し、記事タイトル・公開日・必要本文を取得する |
| API-002 | Jev Judgment（Jev判定） | 指導有用度Score・対象レベル・記事カテゴリを取得する |

連携方式は [05_ARCHITECTURE_DESIGN.md](./05_ARCHITECTURE_DESIGN.md) に記載する。

### 5.5 Data Overview（データ種別・件数規模の概要）

| Data Type（データ種別） | Estimated Volume（想定件数・規模） | Notes（備考） |
|---|---|---|
| Article Markdown（記事Markdown） | 対象日判定を通過した記事（最終記事URL）1件につき1ファイル。件数は利用者の入力件数に依存し、規模の指定はない | 保存項目は [03_DATA_AND_SECURITY_DESIGN.md](./03_DATA_AND_SECURITY_DESIGN.md) |

データベースは使用しない。

### 5.6 Mapping to Request Definition（要求定義との対応マッピング）

| User Story ID（ユーザーストーリー ID） | Functional Requirement ID（対応する機能要件 ID） |
|---|---|
| US-001 | FR-001, FR-002, FR-003, FR-013 |
| US-002 | FR-004, FR-005, FR-006, FR-007 |
| US-003 | FR-008, FR-009, FR-010, FR-011 |
| US-004 | FR-002, FR-012, FR-013, FR-014, FR-016 |
| US-005 | FR-006, FR-014, FR-015 |
| US-006 | FR-017, FR-018 |
| US-007 | FR-019, FR-020 |

---

## 6. Open Issues（未決事項）

| ID | Open Issue（未決事項） | Owner（担当者） | Due Date（期限） | Status（ステータス） |
|---|---|---|---|---|
| O-01 | 記事カテゴリ体系。§5.1.3 の10分類は仮定であり、実運用後に利用者が判断する。`jev_category` が単一値であることは確定している | Takashi Oikawa | 未定 | OPEN |

---

## 7. Handoff to Detail Design（詳細設計への引き継ぎ）

- 公開日の補完は禁止である。タイムゾーン付きの日時は JST へ変換し、日付だけの場合は明示された日付を使う
- 登録済みの記事でも対象日判定を毎回行う。対象外になった記事を再入力だけを理由に更新しない
- Jev判定と人間評価は独立している。再判定で人間評価を変えない。`processed` は初回処理日を保持する
- 記事カテゴリ体系は仮定である。実装でカテゴリ一覧を確定仕様として扱わず、変更は利用者の判断を待つ
