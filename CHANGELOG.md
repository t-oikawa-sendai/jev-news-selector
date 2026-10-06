<!--
Program Name: jev-news-selector CHANGELOG
Language: Markdown
Function: jev-news-selectorの変更履歴正本
Created: 2026-10-06
Last Updated: 2026-10-06
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
| Last Updated（最終更新日） | 2026-10-06 |
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
