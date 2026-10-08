<!--
Program Name: jev-news-selector CURRENT
Language: Markdown
Function: jev-news-selectorの目的・完了・現在地点・次作業・阻害要因を管理する
Created: 2026-10-06
Last Updated: 2026-10-08
Author: Takashi Oikawa
AI: Cursor
Memo: Canonical Sourceは solacom_main の project-notes/CURRENT_TEMPLATE.md。Runtime側に CURRENT_TEMPLATE.md を作成しない
-->

# CURRENT

<!-- Document Info（文書情報） -->
| Item（項目） | Value（値） |
|---|---|
| Document ID（文書ID） | JNS-CURRENT-001 |
| Version（バージョン） | 0.1 |
| Status（ステータス） | Draft |
| Created Date（作成日） | 2026-10-06 |
| Last Updated（最終更新日） | 2026-10-08 |
| Owner（管理者） | Takashi Oikawa |
| Related Documents（関連文書） | ../README.md / ../CONSTITUTION.md / ../AGENTS.md / ../CHANGELOG.md / ../docs/design/README.md |

---

## Purpose（目的）

Repository Purpose: `DEVELOPMENT`

SDDに基づき Repository固有の設計文書を整備し、Userレビューと承認を経て実装引き継ぎへ進む。

## Completed（完了）

- Repositoryを project-bootstrap から作成済み（初回commit `4e938e8`）
- Phase A 事前分析完了
- Phase B Repository固有文書10件のDraft原稿を作成し、未承認のままレビュー共有のため commit `98a6533` で共有済み。共有は設計承認・実装許可ではない
- 2026-10-06、Solution Partnerが共有commit `98a6533` の10文書を横断レビューした。結果は設計FAIL。レビュー完了は是正完了を意味しない
- 2026-10-06、Draft全文是正をローカル作業ツリーで実施した。未commit・未push
- 2026-10-06 21:45:33 JST 取得のレビュー資料（`jev-news-selector-phase-b-correction-review-20261006.md`、ZIP `jev-news-selector-review-20261006-214533.zip`、差分基準 `98a6533f65064b76b0e304c7ae8ee03d0a5833fe`）について、Solution Partnerが10文書の全文・差分・確定仕様を照合した。主要是正は確認済みである。設計全体の承認ではない
- 2026-10-08、承認済み変更予定一覧に基づき、決定事項と暫定採用の整備をローカル作業ツリーで実施した。未commit・未push
- 2026-10-08、追加承認に基づき、04の処理フロー、05の構成とデータの流れ、06の運用順序をMermaid図にした。READMEと設計Indexから04と05の図へリンクした。mermaid-cli 11.12.0 でPNGを生成し、構文、文字の途中折れ、矢印の向きを確認した。この確認は再レビューでも設計承認でもない
- 2026-10-08、Solution Partnerが図整備後の10文書を再レビューした（レビュー資料 `jev-news-selector-diagram-rereview-20261008.md`、ZIP `jev-news-selector-review-20261008-164732.zip`、差分基準 `98a6533f65064b76b0e304c7ae8ee03d0a5833fe`）。結果は要是正（FAIL）。04の再処理の図とSC-004から、記事情報の再取得（今回の最新タイトル・必要本文の取得）と、最終記事URLによる既存Markdownの特定が抜けていた。再レビューの完了は是正完了・設計承認を意味しない
- 2026-10-08、再レビューで承認された限定是正をローカル作業ツリーで実施した。04 §5.2 の図と注記、§5.4 SC-004、§7 に、最新記事情報の取得、既存Markdownの特定、新規・登録済みの両方での公開日の整合を明示した。設計Index目次§2のリンクを、GitHubが生成した見出しIDへ合わせた。修正した図は mermaid-cli 11.12.0 で描画を確認した。未commit・未push
- 2026-10-08、Solution Partnerが限定是正後の資料（ZIP `jev-news-selector-review-20261008-180248.zip`、差分基準 `98a6533f65064b76b0e304c7ae8ee03d0a5833fe`）を実差分で再レビューした（レビュー資料 `jev-news-selector-diagram-rereview-20261008.md` §8）。結果は前回の限定是正 PASS。04の記事情報取得の欠落、公開日条件の図示、SC-004との不整合の解消が確認された。設計全体・実装・commit・pushの承認ではない
- 2026-10-08、同レビュー資料 §7 の追加承認に基づき、README §6 にデータの流れの概要図を配置した（詳細図の正本は05のまま。04・05への図リンクは維持）。04 §5.4 SC-001 に、新規記事であることの確認、今回の最新タイトル・必要本文の取得、使う公開日の適格性確認を明記した。README の概要図と04 Article Diagram は mermaid-cli 11.12.0 で描画を確認した。未commit・未push
- 2026-10-08、Solution Partnerが追加整備後の資料（ZIP `jev-news-selector-review-20261008-182130.zip`、SHA-256 `835f9544865d52e4dcde39c915ceaa4732d24d3d6b77c93975f47179c4ec7a62`、差分基準 `98a6533f65064b76b0e304c7ae8ee03d0a5833fe`）を実差分で再レビューした（レビュー資料 `jev-news-selector-diagram-rereview-20261008.md` §9）。結果は PASS。README §6 の概要図と04 SC-001 の補足は承認範囲内であり、今回の決定事項反映・図整備・限定是正・追加整備について内容の追加修正は不要と判定された。設計全体の承認・実装開始許可・commit・pushの指示ではない
- 2026-10-08、Userの明示指示（「ここでPush 実際のGithubで確認する」。レビュー資料 `jev-news-selector-diagram-rereview-20261008.md` §11）に基づき、10文書を未承認Draftとして共有commit `3f6da3304c83d800509b7671f922631731b1c0c2`（`docs: share revised news selector design draft`）にまとめ、`main` へpushした。push直後、ローカルHEAD・origin/main・GitHub mainは同commitで一致し、作業ツリーはcleanだった。同commitの GitHub Actions `Validate Documents` は completed / success（[run 37767574862](https://github.com/t-oikawa-sendai/jev-news-selector/actions/runs/37767574862)）。設計承認・実装開始許可ではない
- 2026-10-08、共有commit `3f6da33` のGitHub上の表示を、ブラウザで確認した。ルートREADME §6 の概要図は描画された。README §6 の4つの図リンク（入口の図・記事ごとの図・構成の図・データの流れ）と設計Index§2の目次リンクは、クリックで目的のファイルと見出しへ移った。04 Article Diagram と05 Data Flow Diagram は、文字の欠け・重なりがなく、矢印と経路を追えた。GitHubのMermaid描画は、日本語ラベルの折返し位置が mermaid-cli のPNGと異なる（例：「Markdown生 / 成・更新」）。文字は欠けていないため、修正していない。04 `#entry-diagram` と05 `#data-flow-diagram` では、クリック後にMermaid描画で高さが変わり、見出しが画面上端より上へずれた。遷移先のファイルと見出しは正しい。図・リンクの修正は行っていない
- 2026-10-08、設計担当が GitHub main `d55df186c8bc856e2ae765dc8f887fd4af42b6f7` の最終10文書と commit 差分を確認した（レビュー資料 `jev-news-selector-diagram-rereview-20261008.md` §13）。結果は PASS。182130 ZIP の内容レビュー PASS を維持する。設計全体の承認・実装開始許可ではない。本セッション開始時に、ローカル HEAD・origin/main・GitHub main が同じ SHA であることを確認した
- 2026-10-08、Userの明示指示（Userを指す旧表示を `User` に統一、全文書）に基づき、Git管理対象の14 Markdown文書の表示を統一した。保存キー `human_decision` / `human_score`、`jev_*`、`published`、`processed`、`adopted` / `rejected`、仕様ID、O-01〜O-06 の状態、処理条件は変更していない。中央正本は変更していない。`AGENTS.md`・`CONSTITUTION.md`・`docs/NEW_REPOSITORY_SETUP_GUIDE.md`・`docs/standards/DOCUMENT_GOVERNANCE_STANDARD.md` は配布コピーの表記だけを変えており、中央正本との一致は未確認である。未commit・未push。表記統一後の実差分レビューは未実施であり、PASSではない
- 2026-10-08、Userの明示指示により、ルート `README.md` §1 第1段落を、取得、Jev判定、Markdown保存の順が分かる文章へ置き換えた。見出しと、後続のGoogleニュースRSS・入口条件・公開日条件の段落は変更していない。仕様変更ではない。未commit・未push。この文章修正を含む作業ツリー差分のレビューは未実施であり、過去のPASSをこの判定へ転用しない

## Current（現在）

- 設計は未承認であり、プロジェクト固有の10文書は Version 0.1 / Draft である。GitHub `main` は状態記録commit `d55df186c8bc856e2ae765dc8f887fd4af42b6f7` である。共有は設計承認ではない
- Userを指す表示の `User` への統一と、ルート `README.md` §1 第1段落の文章修正は、作業ツリー上の未commit差分である。基準稿 `d55df18` に対するレビュー資料 §13 の PASS と、この差分のレビューは別である。後者は未実施であり、PASSではない。過去のPASSをこの判定へ転用しない
- 中央正本は変更していない。配布コピーに表記差分がある。中央正本との一致は未確認であり、IDENTICAL / PASS ではない
- 撤回事項：Userが記事を探す、選ぶ、URLをコピーする、ターミナルへURLを入力する仕様は、Userの明示により撤回済み。これに伴い US-001 / FR-001 / SCR-001 を失効とし、IDを別仕様へ転用しない
- 2026-10-06、Userが次の3点を決定した（根拠：[Issue #2](https://github.com/t-oikawa-sendai/jev-news-selector/issues/2)）。設計全体の承認ではない
  - 起動：Userが任意の時刻にBotを手動起動する。定期自動起動は採用しない。URL入力を伴わせない
  - Jev Score保存値：評価基準は0〜4の5段階を維持し、Jevが返した小数値をそのまま `jev_score` へ保存する。丸めない
  - 再処理時の公開日：対象日判定を通過した再処理では、`published` と本文の公開日表示を最新の取得値へ更新する。`processed`・初回処理日フォルダ・User評価は保持する
- 2026-10-08、Userが次を決定した（根拠：[Issue #3](https://github.com/t-oikawa-sendai/jev-news-selector/issues/3)）。設計全体の承認でも、RSSの検証完了でもない
  - ニュース取得：GoogleニュースのRSS方式を採用し、検証する
  - 入口：分野・検索語で対象を絞り、検証用件数上限を併用する
  - 検証用件数上限：全検索語の合計で1回最大50件。超過分はその回では無視し、Jev処理へ回さない
- 入口の分野・検索語は暫定採用済みである。管理は [02_REQUIREMENTS_DEFINITION.md](../docs/design/02_REQUIREMENTS_DEFINITION.md) §5.1.6。具体一覧は原記録未復元であり、本文で補完していない
- O-05 の台帳状態は OPEN のままである。Userから記事情報抽出方式の暫定採用を指摘する発言がある。具体値は原記録未復元である。再選定が必要とは断定しない
- 図整備後の再レビュー（164732 ZIP）の FAIL は、限定是正後の再レビュー（180248 ZIP）で解消が確認された（前回の限定是正 PASS）。その後の追加整備（README §6 の概要図、04 SC-001 の補足）も、追加整備後の再レビュー（182130 ZIP）で PASS となった。今回の設計書整備の内容レビューは完了している。過去の FAIL と再レビュー待ちは上記 Completed の履歴として残す。処理フローとデータの流れはMermaid図へ更新済みである。F-ID / R-ID の正式台帳はなく、入口の決定は ID未登録である

## Next（次）

- User表記統一と README §1 第1段落の文章修正を含む作業ツリー差分の実レビュー。基準稿 `d55df18` の §13 PASS を、この差分の PASS として扱わない。結果はレビュー資料と [Issue #3](https://github.com/t-oikawa-sendai/jev-news-selector/issues/3) へ記録される
- 分野・検索語の具体一覧と、O-05 の具体方式の原記録の再取得。再取得まで本文へ補完しない
- 設計担当による分類管理の整理。実装担当は新規 F/O/R-ID を採番しない
- 設計承認後の実装引き継ぎ準備
- 重要な後続課題：CURRENT.mdの記録・更新運用を有効にする改善を検討する。未着手（[Issue #1](https://github.com/t-oikawa-sendai/jev-news-selector/issues/1)）。今回は新しい運用ルールを制定しない

## Blockers（阻害要因）

- 設計全体は未承認である。形式検査の成功は設計承認を意味しない。再レビューと保留事項が残る間は設計承認・実装引き渡しへ進めない
- User表記統一と README §1 の文章修正を含む commit・push は、この差分の実レビュー後の明示指示まで行わない。以前のDraft共有の指示は、この差分へ拡張しない
- この作業ツリー差分の実レビューは未実施である。レビュー資料 §13 の PASS は、表記統一前の `d55df18` に対する判定であり、今回の判定へ転用しない
- GoogleニュースRSSは採用済みであり、検証は未完了である。RSSのURLと使用ライブラリは未確認である
- 入口の分野・検索語は暫定採用済みである。具体一覧は原記録未復元である。未決へは戻していない
- O-05 は OPEN である。具体的な抽出方式は原記録未復元である。解決済みにはしていない。再選定が必要とは断定しない
- 起動の具体的なUI・コマンド形式は未定（起動方法が任意時刻の手動起動であることは決定済み）
- 再処理で記事タイトルが変わった場合のファイル名の扱いが未確認
- ファイル名に使えない文字を含むタイトルの扱いが未確認
- 記事取得・Jev判定・保存に失敗した場合の扱いが未確認。再試行・ログ・監視・バックアップを独自に決めない
- データベースの採否は確定していない。Markdown保存であることだけを根拠に確定しない
- 上記のうち既存 O-01〜O-06 に該当しない事項は ID未登録である。F-ID / R-ID の正式台帳がないため、FROZEN と REJECTED の全件突合は成立していない。整理は設計担当の変更一覧で扱う。Issue #1 とは別である

## Related Decisions（関連Decision）

- なし
