# UI and Flow Design（UI・フロー設計）

<!-- Document Info（文書情報） -->
| Item（項目） | Value（値） |
|---|---|
| Document ID（文書ID） | UI-001 |
| Version（バージョン） | 0.1 |
| Status（ステータス） | Draft |
| Created Date（作成日） | 2026-10-06 |
| Last Updated（最終更新日） | 2026-10-06 |
| Owner（管理者） | Takashi Oikawa |
| Related Documents（関連文書） | README.md / 02_REQUIREMENTS_DEFINITION.md / 03_DATA_AND_SECURITY_DESIGN.md / 05_ARCHITECTURE_DESIGN.md / 06_OPERATION_AND_HANDOFF.md |

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

本文書は、`jev-news-selector` の利用者操作と処理フローを定義する正本である。初期版のUIはターミナルであり、本文書はGUI画面を定義しない。

読者は、利用者・設計担当・実装担当である。

---

## 2. Scope（対象範囲）

- 利用者による記事選択からターミナルへのURL入力までの操作
- URL入力から保存・更新までの処理フロー
- 対象外記事の分岐
- Jev判定と保存処理の流れ
- 登録済み記事を入力した場合の流れ（再処理）
- 初期調整期間における人間評価の位置付け

---

## 3. Out of Scope（対象外範囲）

- GUI画面、Webフォーム、ブラウザ拡張、人間評価専用GUI
- 保存項目・ファイル名規則・更新規則の詳細。[03_DATA_AND_SECURITY_DESIGN.md](./03_DATA_AND_SECURITY_DESIGN.md) を正とする
- 公開日の決定規則の詳細。[02_REQUIREMENTS_DEFINITION.md](./02_REQUIREMENTS_DEFINITION.md) §5.1.4 を正とする

---

## 4. Assumptions（前提条件）

- 利用者は MacBook Air M4 上でニュースを閲覧し、記事を自ら選択する
- 記事の入口は Googleニュースを中心とし、必要に応じてその他サイトを利用する
- Botはターミナルから起動され、記事URLを受け付ける

---

## 5. Definition Details（定義内容）

### 5.1 Screen List — Detail Definition（画面一覧・詳細定義）

本Botには GUI 画面がない。利用者との接点はターミナルのみである。

| Screen ID（画面ID） | Screen Name（画面名） | Input Items（入力項目） | Output Items（出力項目） | Main Operations（主要操作） | Notes（備考） |
|---|---|---|---|---|---|
| SCR-001 | Terminal（ターミナル） | 記事URL（入力URL） | 処理結果（対象外記事の通知を含む） | コピーした記事URLを貼り付けて入力する | 表示文言は未決（実装段階で決定） |

### 5.2 Screen Transition and Business Flow（画面遷移図・業務フロー）

#### User Operation（利用者操作）

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
```

#### Processing Flow（処理フロー）

```text
URL入力（入力URL）
↓
最終記事URL取得
↓
記事公開日取得
↓
公開日を特定できるか？
├─ NO ─→ 対象外（Jev判定・新規保存・更新なし）
│
└─ YES
    ↓
  JST基準で対象日判定
    ↓
  実行日または前日か？
    ├─ NO ─→ 対象外（Jev判定・新規保存・更新なし）
    │
    └─ YES
        ↓
      登録済みの最終記事URLか？
        ├─ NO（新規記事）
        │   ↓
        │ 記事タイトル・必要本文取得
        │   ↓
        │ Jev判定
        │   ↓
        │ Markdown生成
        │   ↓
        │ 当日の処理日フォルダに同名ファイルがあるか？
        │   ├─ NO ─→ 記事タイトル.md を新規作成
        │   └─ YES（別の最終記事URL）─→ 記事タイトル_<URL由来短縮識別子>.md を新規作成
        │
        └─ YES（再処理）
            ↓
          記事情報再取得
            ↓
          Jev再判定
            ↓
          既存Markdown更新（初回処理日フォルダのまま。processed と人間評価は保持）
```

- 登録済みの記事でも、対象日判定は毎回行う。対象期間外になった記事を、再入力だけを理由に更新しない
- 公開日は、タイムゾーン付きの日時なら Asia/Tokyo へ変換した日付、日付だけなら明示された日付とする（[02_REQUIREMENTS_DEFINITION.md](./02_REQUIREMENTS_DEFINITION.md) §5.1.4）
- Jev Score による分岐はない。対象日判定を通過した記事は全件保存する

### 5.3 Wireframes and Layout Policy（主要画面のワイヤーフレーム・レイアウト方針）

本文書では対象外。理由: GUI画面がなく、ターミナルでの入出力のみであるため。

### 5.4 Operation Flow and User Scenarios（操作フロー・ユーザーシナリオ）

| Scenario ID（シナリオID） | Operation Name（操作名） | Steps（操作手順） |
|---|---|---|
| SC-001 | 新規記事の保存 | 1. 記事を選びURLをコピー → 2. ターミナルからURLを入力 → 3. 最終記事URLを取得 → 4. 対象日判定を通過 → 5. Jev判定 → 6. `Bot News/<処理日>/記事タイトル.md` を作成 |
| SC-002 | 公開日を特定できない記事 | 1. URLを入力 → 2. 公開日を取得・特定できない → 3. 対象外として処理を終了（Jev判定・保存・更新なし） |
| SC-003 | 対象期間外の記事 | 1. URLを入力 → 2. 公開日（JST）が Bot実行日・前日のいずれでもない → 3. 対象外として処理を終了（Jev判定・保存・更新なし） |
| SC-004 | 登録済み記事の再入力（対象期間内） | 1. 登録済みの記事のURLを入力（入力URLは初回と異なってもよい）→ 2. 最終記事URLを取得 → 3. 対象日判定を通過 → 4. 最終記事URLで既存Markdownを特定し、記事情報再取得・Jev再判定 → 5. 既存Markdownを更新（新しい処理日フォルダへ移動・複製しない） |
| SC-005 | 登録済み記事の再入力（対象期間外） | 1. 登録済みの記事のURLを入力 → 2. 公開日（JST）が対象期間外 → 3. 既存Markdownを更新しない |
| SC-006 | 同一処理日・同タイトル・別URL | 1. URLを入力 → 2. 処理日フォルダに同名ファイルがあり、最終記事URLが異なる → 3. `記事タイトル_<URL由来短縮識別子>.md` として新規作成（既存ファイルを上書きしない） |
| SC-007 | 人間評価の記録（初期調整期間） | 1. 保存された記事Markdownを確認 → 2. `human_decision` と `human_score` を記録（入力方法は O-03） |

#### Position of Human Evaluation（人間評価の位置付け）

- 人間評価は初期調整期間のみ行う
- 人間評価は保存処理とは別の利用者操作であり、Jev判定の結果を変更しない
- Jev再判定は人間評価を変更しない
- Jev判定が十分安定したと利用者が判断した時点で、新しい記事への日常的な人間評価入力を終了する。記録済みの人間評価は残す。終了後も処理フローは変わらず、全件保存を続ける
- 運用上の扱いは [06_OPERATION_AND_HANDOFF.md](./06_OPERATION_AND_HANDOFF.md) を正とする

### 5.5 Validation and Error Handling Policy（バリデーション・エラーハンドリング方針 / UI層）

| Target（対象） | Validation Rules（バリデーションルール） | Error Message / Display Policy（エラーメッセージ・表示方針） |
|---|---|---|
| 記事公開日 | 取得できない・特定できない・推測しなければ日付を決められない場合は対象外。Bot実行日・取得日・更新日・推測値で補完しない | 対象外であることを利用者へ表示する。文言は未決（実装段階で決定） |
| 対象日 | 公開日（JST）が Bot実行日または前日でない場合は対象外。登録済みの記事も同じ | 対象外であることを利用者へ表示する。文言は未決（実装段階で決定） |

### 5.6 Accessibility and Responsive Design Policy（アクセシビリティ・レスポンシブ対応方針）

本文書では対象外。理由: GUI画面がなく、ターミナルでの入出力のみであるため。

---

## 6. Open Issues（未決事項）

| ID | Open Issue（未決事項） | Owner（担当者） | Due Date（期限） | Status（ステータス） |
|---|---|---|---|---|
| O-03 | 人間評価入力方法。初期調整期間の `human_decision` / `human_score` をどの操作で入力するか。専用GUIは要求されていない | Takashi Oikawa | 未定 | OPEN |

#### Implementation-Stage Items（実装段階で決定する事項）

| Item（項目） | Related Section（関連箇所） |
|---|---|
| 対象外記事を表示するメッセージ文言 | §5.1 / §5.5 |

---

## 7. Handoff to Detail Design（詳細設計への引き継ぎ）

- 初期版のUIはターミナルのみである。GUIを実装しない
- 対象日判定は登録済み判定より先に行う。対象外記事は Jev判定・新規保存・更新を行わない
- 登録済みの記事は再取得・再判定して既存Markdownを更新する。処理日フォルダへ移動・複製しない
