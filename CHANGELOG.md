<!--
Program Name: jev-news-selector CHANGELOG
Language: Markdown
Function: jev-news-selectorの変更履歴正本
Created: 2026-10-06
Last Updated: 2026-10-08
Author: Takashi Oikawa
AI: Cursor
Memo: Runtime /CHANGELOG.md。推測履歴を記載しない。Runtime側に CHANGELOG_TEMPLATE.md は作成しない
-->

# CHANGELOG

<!-- Document Info（文書情報） -->
| Item（項目） | Value（値） |
|---|---|
| Document ID（文書ID） | CHANGELOG-001 |
| Version（バージョン） | 0.1 |
| Status（ステータス） | Draft |
| Created Date（作成日） | 2026-10-06 |
| Last Updated（最終更新日） | 2026-10-08 |
| Owner（管理者） | Takashi Oikawa |
| Related Documents（関連文書） | [CONSTITUTION.md](./CONSTITUTION.md) / [AGENTS.md](./AGENTS.md) / [README.md](./README.md) / [docs/design/README.md](./docs/design/README.md) |

---

## Purpose（目的）

本ファイルは、`jev-news-selector` の変更履歴正本である。

本Repository内の Markdown 文書の作成・更新履歴を一元管理する。各文書内に変更履歴の章を設けない。

推測による履歴は記載しない。

## What to Record（記録対象）

利用者・開発者・運用担当者・レビュー担当者の判断に影響する重要変更を記録する。

意味・仕様・運用・構成に影響しない軽微な変更（明白な誤字、空白調整など）は原則記録不要とする。ただし、コマンド・パス・設定値・日付・バージョン・識別子など、判断へ影響する修正は `Fixed` として記録する。

Governance導入Baselineは、Governance導入成功後に記録する。導入前に成功した事実として記録しない。

## Category Definitions（変更分類）

| Category（分類） | Japanese（日本語） | Usage（用途） |
|---|---|---|
| Added | 追加 | 新しい機能、章、文書、運用項目 |
| Changed | 変更 | 既存仕様、構成、手順の変更 |
| Fixed | 修正 | 誤り、不整合、不具合の修正 |
| Removed | 削除 | 機能、記述、文書の廃止 |
| Security | セキュリティ | セキュリティまたは個人情報保護上の変更 |

Git 履歴は差分確認の補助として利用する。CHANGELOG の代替とはしない。

## Change History（変更履歴）

新しい履歴を上、古い履歴を下に記載する。

| Version（バージョン） | Date（日付） | Document（文書） | Category（分類） | Changes（変更内容） | Author（作成者） |
|---|---|---|---|---|---|
| 0.1 | 2026-10-08 | `project-notes/CURRENT.md` / `CHANGELOG.md` | Changed | 状態記録を更新。利用者の明示指示により、10文書を未承認Draftとして共有commit `3f6da33` でGitHub `main` へpushしたことを記録した。同commitの Validate Documents は success だった。GitHub上で確認した結果も記録した。README §6 概要図の描画、図リンク4件と設計Index§2目次リンクのクリック遷移、04 Article Diagram と05 Data Flow Diagram の表示である。Mermaidの折返し位置の違いと、遷移後の見出し位置のずれも記録した。表示・リンクの修正なし。設計本文・図の変更なし。新規ID・分類変更なし。Version 0.1 / Draft のまま。設計承認・実装は未実施 | Takashi Oikawa |
| 0.1 | 2026-10-08 | `project-notes/CURRENT.md` / `CHANGELOG.md` | Changed | 状態記録を更新。追加整備後の再レビュー（182130 ZIP）が PASS となり、今回の設計書整備の内容レビューが完了したことを記録した。追加整備後の再レビューを現在の次作業と阻害要因から外し、過去の FAIL と再レビュー待ちの履歴は残した。GitHub上のREADME Mermaid表示とブラウザでのリンククリックが未検証であることを記録した。設計本文・図の変更なし。新規ID・分類変更なし。Version 0.1 / Draft のまま。設計承認・実装・commit・pushは未実施 | Takashi Oikawa |
| 0.1 | 2026-10-08 | `README.md` / `docs/design/04_UI_AND_FLOW_DESIGN.md` / `project-notes/CURRENT.md` / `CHANGELOG.md` | Changed | 限定是正後の再レビュー（前回の限定是正 PASS）で承認された追加整備を実施した。README §6 にデータの流れの概要図と短い説明を配置した。詳細なデータの流れは05、処理の分岐は04を正とし、既存の図リンクは残した。04 §5.4 SC-001 に、新規記事であることの確認、今回の最新タイトル・必要本文の取得、使う公開日の適格性確認を明記した。図と注記に合わせた補足であり、新しい処理要件ではない。CURRENTに再レビュー結果と追加整備の状態を記録した。新規ID・分類変更なし。Version 0.1 / Draft のまま。追加整備後の再レビュー・設計承認・実装・commit・pushは未実施 | Takashi Oikawa |
| 0.1 | 2026-10-08 | `docs/design/04_UI_AND_FLOW_DESIGN.md` / `docs/design/README.md` / `project-notes/CURRENT.md` / `CHANGELOG.md` | Fixed | 図整備後の再レビュー（FAIL）で承認された限定是正を実施した。04 §5.2 の図と注記、§5.4 SC-004、§7 に、02 FR-015 / §5.1.5・03の再処理更新規則・06 HO-005 にある記事情報の再取得を戻した。対象日判定の後に最終記事URLで既存Markdownを特定し、新規・登録済みとも今回の最新タイトル・必要本文を取得してJev判定に使う。使う公開日の条件は新規・登録済みの両方に適用する。再取得はHTTPの二重呼出しを要求しない。設計Index目次§2のリンクを、GitHubが生成した見出しIDへ合わせた。CURRENTに再レビュー結果と是正状態を記録した。新規ID・分類変更なし。Version 0.1 / Draft のまま。是正後再レビュー・設計承認・実装・commit・pushは未実施 | Takashi Oikawa |
| 0.1 | 2026-10-08 | `README.md` / `docs/design/README.md` / `docs/design/04_UI_AND_FLOW_DESIGN.md` / `docs/design/05_ARCHITECTURE_DESIGN.md` / `docs/design/06_OPERATION_AND_HANDOFF.md` / `project-notes/CURRENT.md` / `CHANGELOG.md` | Changed | 追加承認に基づき、処理フロー、構成、データの流れ、運用順序のASCII図をMermaid図へ置き換えた。詳細な処理図は04、構成とデータの流れは05に置き、READMEと設計Indexからはその図へリンクした。mermaid-cli 11.12.0 でPNGを生成し、描画を確認した。Version 0.1 / Draft のまま。再レビュー・設計承認・実装・commit・pushは未実施 | Takashi Oikawa |
| 0.1 | 2026-10-08 | `README.md` / `CHANGELOG.md` / `project-notes/CURRENT.md` / `docs/design/` 7文書 | Changed | 承認済み変更予定に基づき整備した。GoogleニュースRSSの採用（検証は未完了）、入口の分野・検索語の暫定採用（具体一覧は原記録未復元。02 §5.1.6 で管理し、06と設計Indexから参照）、検証用上限（全検索語合計で1回最大50件、超過分はその回では無視）、04の再処理で使う公開日と対象日判定の一致、02・06における判定指示の調整と確定仕様の変更の境界、O-05のOPEN維持と暫定採用の指摘・原記録未復元の併記、CURRENTの状態区分を更新した。Version 0.1 / Draft のまま。設計承認・実装・commit・pushは未実施 | Takashi Oikawa |
| 0.1 | 2026-10-06 | `project-notes/CURRENT.md` | Changed | 状態記録を更新。Solution Partnerによる共有commit `98a6533` の横断レビュー（設計FAIL）、Draft全文是正の実施状態（未commit・未push・是正後レビュー未実施）、Userの3点決定（Issue #2）、記事取得の手段・範囲等のID未登録の保留事項、後続課題（CURRENT.md記録運用の改善、未着手、Issue #1）を記録 | Takashi Oikawa |
| 0.1 | 2026-10-06 | `docs/design/` 7文書 / `README.md` | Changed | Userの決定（Issue #2）を反映。起動を利用者による任意時刻の手動起動とし定期自動起動を採用しない、`jev_score` はJevが返した小数値をそのまま保存し丸めない、対象日判定を通過した再処理で `published` と本文の公開日表示を最新の取得値へ更新する | Takashi Oikawa |
| 0.1 | 2026-10-06 | `docs/design/` 7文書 / `README.md` | Fixed | 撤回済みの人間による記事の探索・選択・URLコピー・URL手入力の前提を有効仕様から除去し、全文を再作成。US-001 / FR-001 / SCR-001 を失効とし転用禁止を明記。記事取得の手段・範囲、起動のUI・コマンド形式、再処理時のファイル名、ファイル名に使えない文字の扱い、処理失敗時の扱い、データベースの採否を未確認として CURRENT.md の Blockers へ参照。Version 0.1 / Draft、未承認のまま | Takashi Oikawa |
| 0.1 | 2026-10-06 | `project-notes/CURRENT.md` | Changed | 状態記録を更新。Userによる設計全文の誤り指摘、設計未承認、是正未完了、GitHubでのレビュー共有を記録。「レビュー指摘の反映完了」を完了事項から除外 | Takashi Oikawa |
| 0.1 | 2026-10-06 | `README.md` / `CHANGELOG.md` / `project-notes/CURRENT.md` / `docs/design/` 7文書 | Changed | Userの明示承認により、未承認Phase B DraftをGitHubでのレビュー共有のためcommit対象とした。設計承認・実装許可を意味しない | Takashi Oikawa |
| 0.1 | 2026-10-06 | `docs/design/06_OPERATION_AND_HANDOFF.md` | Added | Repository固有の運用・実装引き継ぎ設計（OPS-001）を初期作成。初期調整期間、Jev安定判断後の運用、自動選別の導入手順を定義 | Takashi Oikawa |
| 0.1 | 2026-10-06 | `docs/design/05_ARCHITECTURE_DESIGN.md` | Added | Repository固有のアーキテクチャ設計（ARCH-001）を初期作成。未決事項 O-04 / O-05 を記載 | Takashi Oikawa |
| 0.1 | 2026-10-06 | `docs/design/04_UI_AND_FLOW_DESIGN.md` | Added | Repository固有のターミナル操作・処理フロー設計（UI-001）を初期作成。登録済み記事の再処理フローを定義。未決事項 O-03 を記載 | Takashi Oikawa |
| 0.1 | 2026-10-06 | `docs/design/03_DATA_AND_SECURITY_DESIGN.md` | Added | Repository固有のデータ・保存・セキュリティ設計（DATA-001）を初期作成。YAML frontmatter、最終記事URLによる一意規則、再処理時の更新規則を定義。未決事項 O-02 / O-06 を記載 | Takashi Oikawa |
| 0.1 | 2026-10-06 | `docs/design/02_REQUIREMENTS_DEFINITION.md` | Added | Repository固有の要件定義（REQS-001）を初期作成。公開日の JST 規則、`jev_category` 単一値、再処理要件を定義。未決事項 O-01 を記載 | Takashi Oikawa |
| 0.1 | 2026-10-06 | `docs/design/01_REQUEST_DEFINITION.md` | Added | Repository固有の要求定義（REQ-001）を初期作成 | Takashi Oikawa |
| 0.1 | 2026-10-06 | `docs/design/README.md` | Added | Repository固有の設計書入口（README-001）を初期作成 | Takashi Oikawa |
| 0.1 | 2026-10-06 | `project-notes/CURRENT.md` | Added | Repository固有の現在地点（JNS-CURRENT-001）を初期作成 | Takashi Oikawa |
| 0.1 | 2026-10-06 | `README.md` | Added | Repository固有README（JNS-README-001）を初期作成 | Takashi Oikawa |
| 0.1 | 2026-10-06 | `CHANGELOG.md` | Added | 本Repositoryの変更履歴正本として初期作成 | Takashi Oikawa |
