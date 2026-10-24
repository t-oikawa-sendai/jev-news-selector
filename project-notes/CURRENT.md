<!--
Program Name: jev-news-selector CURRENT
Language: Markdown
Function: jev-news-selectorの目的・完了・現在地点・次作業・阻害要因を管理する
Created: 2026-10-06
Last Updated: 2026-10-24
Author: Takashi Oikawa
AI: Cursor
Memo: Canonical Sourceは solacom_main の project-notes/CURRENT_TEMPLATE.md。Runtime側に CURRENT_TEMPLATE.md を作成しない
-->

# CURRENT

<details>
<summary>Document Info（文書情報）</summary>

| Item（項目） | Value（値） |
|---|---|
| Document ID（文書ID） | JNS-CURRENT-001 |
| Version（バージョン） | 0.1 |
| Status（ステータス） | Draft |
| Created Date（作成日） | 2026-10-06 |
| Last Updated（最終更新日） | 2026-10-24 |
| Owner（管理者） | Takashi Oikawa |
| Related Documents（関連文書） | ../README.md / ../CONSTITUTION.md / ../AGENTS.md / ../CHANGELOG.md / ../docs/design/README.md |

</details>

---

## Purpose（目的）

Repository Purpose: `DEVELOPMENT`

SDDに基づき Repository固有の設計文書を整備し、Userレビューと承認を経て実装引き継ぎへ進む。

## Completed（完了）

- 2026-10-24、UserのCommit・Push・ローカル同期指示により、設計統合の6文書を`368f107`に記録し、先行する`f758160`とともにGitHub `main`へPushした。GitHub上の`368f107`を確認し、指定作業Cloneと`~/Dev/jev-news-selector`を同Commitへ同期した。設計承認・実装・Jev API実呼出しは行っていない。

- 2026-10-24、Userが決定した初期CLI接続試験の限定条件（既存251件Excel、TypeSafe直接、公式Python SDK、O-01の10カテゴリ候補の試験限定仮使用、タイトルのみ入力）を02・04・05・06へ統合し、初回接続確認と後続のルール・本体検証の境界を整合した。設計はDraftのまま。実装・API実呼出し・試験は未実施。保存・同期の結果は上記の記録を参照。

- 2026-10-23、User指示により、判断特化型AIの比較候補（Jev・Microsoft-Decision-1・Clef／Clef-flash）、利用手順、料金・概算条件・公式出典、JevとMicrosoftのAPI共用条件を05 §6へ記録した。調査記録のみで、採用変更・実装・実API接続・比較試験は未実施。

- 2026-10-23、User指示により、冒頭に文書情報表を持つ13文書を折りたたみ表示へ変更した。表の項目・値は保持し、中央管理コピーも今回の明示指示に基づく表示変更だけを行った。CONSTITUTIONは対象表がないため変更なし。Commit・Pushは未実施。

- 2026-10-23、User承認に基づき、READMEに記事選別の負担とJevの採用理由・比較検証目的を追記し、要求定義01 §5.1と整合した。READMEは概要に絞り、背景・目的の詳細は要求定義01 §5.1、機能・条件の詳細は要件定義02を参照する構成にした。READMEの目次・章番号を更新した。文書修正のみで、実装・比較試験・Commit・Pushは未実施。

- 2026-10-23、User確認により、初期は選別品質ではなくロジックどおりの動作を優先すること、ルールをパーツ分割して組み合わせ検証すること、251件をテスト用と割り切ることを05 §6と06 §5.3へ記録した。固定回答によるロジック確認と実API接続確認を分離する。記録のみ完了し、実装・試験・Commit・Pushは未実施。

- 2026-10-23、User指示によりPython・Jev APIを使うプログラム概要設計を開始し、05 §6へ責務分割・質問・集計・データ・検証の案を追記した。TypeSafe公式API・Python SDK・判定型の資料を確認し、Jevの個別判定とPythonの重み・関係性計算を分離した。実装・API実呼出し・設計承認は未実施。

- 2026-10-23、Userの「リポの設計文書の該当箇所に記載」「CURRENTも忘れずに」という指示に基づき、05 §6へニュース選別の概要設計草案を記録した。251件・77語句を出発点とする方針、3段階のFilter、重み・関係性・二重加点防止、例外・説明・調整、Jev仕様照合前の制約を記載。06 §5.6と設計Indexから参照した。記録の完了であり、設計承認・実装完了ではない。Commit・Pushは未実施。

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

- 初期CLI接続試験はタイトルのみを入力とする3判断（Score・対象レベル・カテゴリ）の回答形式確認である。O-01の10候補は試験限定の仮使用。RSS・本文取得・全件Markdown保存は本体要件として後続に維持する。05 §6と06 §5.3を参照。Version 0.1 / Draftで設計未承認。

- 2026-10-24の設計統合は`368f107`に記録し、先行する`f758160`とともにGitHub `main`へ反映した。指定作業Cloneと`~/Dev/jev-news-selector`はGitHub `main`へ同期した。最終状態は各保存先のHEADで照合する。

- AI比較候補・料金・API共用条件の調査記録を05 §6へ反映済み。接続先・認証情報・認証ヘッダー・モデル指定を切り替える共用案は実接続未検証。Jevの採用は維持。2026-10-23の3文書の変更は`f758160`に記録済みで、2026-10-24にPush済み。

- 文書情報表の折りたたみ変更は05c7433でPush済み（User提示の実行結果）。README背景・Jev比較検証目的の変更はd1d24f5でPush済み（User提示の実行結果）。

- Jevが汎用LLMより一貫した判定を行えるかを、実装を通じて検証する。優位性は未検証。目的の正本は01 §5.1。初期はロジック動作確認を優先し、比較は後続段階とする。README・要求定義・状態記録・履歴の修正はd1d24f5でPush済み（User提示の実行結果）。

- 初期CLIテストの目的はロジックどおりの動作確認。選別品質は徐々に改善する。ルールはパーツ単独と組み合わせで検証し、251件はテスト用として扱う。品質評価用データの厳密化を初期作業の前提にしない。

- 2026-10-23 User方針：初期版はCLIから手動実行し、シンプルな最小機能でテストする。動作確認後に自動化等を追加する。05 §6に3段階を記録し、01・02・04・06と関連記述を整合した。自動実行と記事の自動除外は別扱いとし、全件保存は維持する。

- Python・Jev APIによる概要設計を検討中。05 §6のプログラム案を参照。初期版3判断と将来の選別用質問を分離し、全件保存を維持する。初回CLI試験はTypeSafe直接・公式Python SDKとするが、SDK版・モデル識別子と本体での処理分担は未確定。

- 設計は未承認であり、Version 0.1 / Draft を維持している。2026-10-23にGitHubコネクターで確認した `main` は `42ec0236a5985842d92500509cac2ef65c2c6d06`（`docs: unify User terminology and clarify overview`）。作業開始時のローカルHEADと一致し、作業ツリーはcleanだった。共有は設計承認ではない
- 今回の作業先は `Documents/ChatGPT/☑️jev-news-selector/repository` の独立Clone。`~/Dev/jev-news-selector` もGitHubから早送り同期した。05 §6の選別案は未承認・Jev仕様照合前であり、FR-012の全件保存、Score 0〜4、単一カテゴリ、User評価との分離を維持する。
- Userを指す表示の `User` への統一と、ルート `README.md` §1 第1段落の文章修正は、commit `42ec023` に含まれていることを2026-10-23に確認した。従来の未commit表記は過去の記録である。基準稿 `d55df18` に対するレビュー資料 §13 の PASS と、この差分のレビューは別である。後者は未実施であり、PASSではない。過去のPASSをこの判定へ転用しない
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

- 初回試験の対象ID・指定方法、CLIコマンド・引数、公式SDK版・モデル識別子、鍵の取り扱い、失敗時の扱いを整理する。設計承認後に実装・実API接続を確認し、続いてルールパーツ単独・組み合わせ、実API回答との結合を検証する。

- 動作確認後の比較に向け、同じ記事・判定基準による汎用LLMとの比較方法を具体化する。一貫性と講師判断への適合性を分け、比較対象モデル・測定方法・合否基準を決める。初期CLI動作確認の前提にはしない。

- 各ルールパーツの入出力・実行順・競合順・仮設定と期待結果を具体化し、固定回答による単独／組み合わせテストと実API接続テストの設計を整える。

- CLI最小テストのコマンド・入力形式・質問定義・確認項目を具体化する。その後、手動で一連の動作を確認し、自動化等の後続機能へ進む。

- Python・Jev API案の責務分担と質問をレビューし、入力本文量・質問構成・モデル・重み・関係性ルールを具体化する。APIの実呼出しは未実施。

- 05 §6の概要設計草案とJevの一次仕様・既存設計を照合し、Jevとアプリの責務を整理する。その後に重み・関係性・基準値・例外を具体化する。
- 今回の概要設計案を基に、次段階の詳細化を進める。

- `42ec023`のUser表記統一と README §1 第1段落の文章修正に対する独立レビュー。基準稿 `d55df18` の §13 PASS を、この差分の PASS として扱わない。結果はレビュー資料と [Issue #3](https://github.com/t-oikawa-sendai/jev-news-selector/issues/3) へ記録される
- 分野・検索語の具体一覧と、O-05 の具体方式の原記録の再取得。再取得まで本文へ補完しない
- 設計担当による分類管理の整理。実装担当は新規 F/O/R-ID を採番しない
- 設計承認後の実装引き継ぎ準備
- 重要な後続課題：CURRENT.mdの記録・更新運用を有効にする改善を検討する。未着手（[Issue #1](https://github.com/t-oikawa-sendai/jev-news-selector/issues/1)）。今回は新しい運用ルールを制定しない

## Blockers（阻害要因）

- 初回CLI試験の対象ID・入力ファイル配置・指定形式、CLIコマンド・引数、SDK版・モデル識別子、API失敗時の再試行・継続は未確定。

- 05 §6の一般案はJev仕様との全面照合前。公式API・Python SDK・判定型の確認結果とプログラム案は追記済み。重み・関係性・採否基準値・例外順序・処理分担は未確定であり、自動選別を導入しない。

- 設計全体は未承認である。形式検査の成功は設計承認を意味しない。再レビューと保留事項が残る間は設計承認・実装引き渡しへ進めない
- 過去のUser表記統一と README §1 の文章修正は42ec023で保存済み。今回の設計統合のPushも、設計全体の承認や実装開始許可ではない
- `42ec023`の表記統一等に対する独立レビューは未実施である。レビュー資料 §13 の PASS は、表記統一前の `d55df18` に対する判定であり、今回の設計統合の判定へ転用しない
- GoogleニュースRSSは採用済みであり、検証は未完了である。RSSのURLと使用ライブラリは未確認である
- 入口の分野・検索語は暫定採用済みである。具体一覧は原記録未復元である。未決へは戻していない
- O-05 は OPEN である。具体的な抽出方式は原記録未復元である。解決済みにはしていない。再選定が必要とは断定しない
- 初期版の起動方式はCLIによる手動実行に決定済み。具体的なコマンド・引数・入力形式・表示は未定。自動化は動作確認後の後続段階。
- 再処理で記事タイトルが変わった場合のファイル名の扱いが未確認
- ファイル名に使えない文字を含むタイトルの扱いが未確認
- 記事取得・Jev判定・保存に失敗した場合の扱いが未確認。再試行・ログ・監視・バックアップを独自に決めない
- データベースの採否は確定していない。Markdown保存であることだけを根拠に確定しない
- 上記のうち既存 O-01〜O-06 に該当しない事項は ID未登録である。F-ID / R-ID の正式台帳がないため、FROZEN と REJECTED の全件突合は成立していない。整理は設計担当の変更一覧で扱う。Issue #1 とは別である

## Related Decisions（関連Decision）

- なし
