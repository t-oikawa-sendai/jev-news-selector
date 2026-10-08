<!--
STANDARD_ID: SCAO-AI-GOVERNANCE-CONSTITUTION
STANDARD_VERSION: 1.7
SOURCE: solacom_main/docs/standards/project-bootstrap/CONSTITUTION.md
DISTRIBUTION_MODE: COPY_FROM_CENTRAL_SSOT
LOCAL_EDIT_POLICY: PROHIBITED
-->

# Development Constitution（開発憲法）

## 1. Purpose（目的）

本憲法は、プロジェクトにおける設計・仕様変更・実装・検証・デプロイの統制を定める。

次を恒久的に防止する。

- 確定済み仕様が、実装担当 AI の独自判断により未決事項へ変更される
- 未決事項が根拠なく追加される
- 却下済み仕様が再提案または復活する
- 仕様正本内で、同一事項が「確定」と「未決」の両方に存在する
- 標準文書の配置先を AI または作業者が都度判断し、欠落・誤配置・部分導入が発生する
- 作業報告だけで完了と判断され、実差分の不整合が見逃される
- 内部調査の全過程を通常回答へ混入し、判断に不要な冗長回答を提示する

## 2. Scope（適用範囲）

本憲法は、中央標準を導入した各リポジトリの全参加者に適用する。

- User（プロジェクト責任者）
- Designer（設計担当）
- Implementation Agent（実装担当 AI）
- Reviewer（レビュー担当）
- Operator（運用担当）

機能固有の `SPECIFICATION.md` は各リポジトリ内の正本とする。本憲法はその分類保全ルールおよび標準導入ゲートを定める。

## 3. Roles and Authority（役割と権限）

### 3.1 User

- 業務仕様の最終決定権を持つ
- 確定仕様、未決事項、却下仕様の分類変更を承認する
- 実装・commit・push・deploy の実行可否を判断する

### 3.2 Designer（設計担当）

- 要件整理、設計、技術選定、仕様分類を行う
- 実装担当へ完全版指示書を作成する
- 実差分をレビューする
- 確定仕様、未決事項、却下仕様を ID 管理する

### 3.3 Implementation Agent（実装担当 AI）

- 承認済み指示の範囲だけを編集・実装する
- 仕様分類を独自に変更しない
- 矛盾または不足を発見した場合は停止して報告する
- 自ら仕様を再設計、再評価、一般化しない

## 4. Canonical Source Management（正本管理）

- 中央標準の Canonical Source は `solacom_main/docs/standards/project-bootstrap/` とする
- 各リポジトリへは、定義済み Distribution Mapping により Runtime Artifact を配置する
- 配布は次の原則に従う
  - 中央 Canonical Source
  - 定義済み Distribution Mapping
  - Repository Runtime Artifact
- `AGENTS_SOURCE.md` は `/AGENTS.md` として配布する
- DEVELOPMENT 等の現行 Profile では、`CHANGELOG_TEMPLATE.md` は `/CHANGELOG.md` として配布する。Runtime 側に `CHANGELOG_TEMPLATE.md` を作成してはならない
- DEVELOPMENT 等の現行 Profile では、`scripts/validate-docs.py` は `/scripts/validate-docs.py` として配布する
- DEVELOPMENT 等の現行 Profile では、`.github/workflows/validate-docs.yml` は `/.github/workflows/validate-docs.yml` として配布する
- `/project-notes/CURRENT.md` の Canonical Source は `project-notes/CURRENT_TEMPLATE.md` とする
- DEVELOPMENT 等の現行 Profile では、新規Repositoryへの標準配置 Mapping は次とする

```text
solacom_main/docs/standards/project-bootstrap/project-notes/CURRENT_TEMPLATE.md
→ project-bootstrap/project-notes/CURRENT.md
→ Runtime /project-notes/CURRENT.md
```

- DEVELOPMENT 等の現行 Profile では、Runtime 側に `CURRENT_TEMPLATE.md` を作成してはならない
- `/project-notes/CURRENT.md` は Standard であり、必須Governance文書10へ追加しない。`CURRENT.md` の不存在は Governance導入ゲート違反としない
- LEARNING Profile では、`project-notes/CURRENT_TEMPLATE.md` は `/project-notes/CURRENT.md` として配布する。Runtime 側に `CURRENT_TEMPLATE.md` を作成してはならない
- LEARNING Profile では `CHANGELOG_TEMPLATE.md` および Validation Assets を配布しない
- 通常 Repository では `/CHANGELOG.md` は Repository 固有履歴正本である。LEARNING では `/CHANGELOG.md` を必須としない
- `project-bootstrap` の `/CHANGELOG.md` は明示的例外であり、Distribution Template Artifact である。`project-bootstrap` 自身の変更履歴正本ではない
- Governance / Distribution Source 側の変更履歴正本は `solacom_main/CHANGELOG.md` とする
- ファイルごとの配置先を AI または作業者が判断してはならない
- 機能固有仕様の正本は、作業指示書で指定された `SPECIFICATION.md` のみとする
- 複数の正本が存在する場合、実装担当 AI は編集を停止し報告する

## 5. Specification Classification Preservation（仕様分類保全）

### 5.1 Classification Types（分類種別）

仕様は次の 3 分類で管理する。

| Classification（分類） | ID（識別子） | State（状態） |
| --- | --- | --- |
| Confirmed Specification（確定仕様） | `F-xxx` | `FROZEN` |
| Open Issue（未決事項） | `O-xxx` | `OPEN` |
| Rejected Specification（却下仕様） | `R-xxx` | `REJECTED` |

### 5.2 Classification Authority（分類権限）

- 分類権限はUserおよび設計担当のみが持つ
- 実装担当 AI は分類を変更してはならない
- 確定仕様を未決事項へ降格してはならない
- 未決事項を確定仕様へ昇格してはならない
- 却下仕様を有効仕様へ復活させてはならない
- 実装担当 AI が新規 ID を採番してはならない

### 5.3 Protection of Confirmed Specifications（確定仕様の保護）

- `FROZEN` 仕様を削除しない
- `FROZEN` 仕様を未決化しない
- `FROZEN` 仕様を「案」「方向性」「予定」「要確認」へ変更しない
- 言い換えによる意味変更を行わない
- 条件、対象、例外、責務を削減しない
- 実体確認未完了を理由に、確定済み業務仕様を降格しない
- 業務仕様と実装詳細を混同しない

### 5.4 Open Issue Protection（未決事項の保護）

- 未決事項は設計担当が指定した ID 一覧だけを正とする
- 指定一覧にない未決事項を追加してはならない
- 新しい論点を発見した場合は正本へ追加せず、候補として報告する
- 未決事項の名称を変更し、意味や対象範囲を変えてはならない
- 未決事項を別論点へ置き換えてはならない

### 5.5 Rejected Specification Protection（却下仕様の保護）

- `REJECTED` 仕様を再提案しない
- 却下理由を削除または弱めない
- 却下仕様を別表現で実質的に復活させない
- 再検討が必要に見える場合は変更せず報告する

### 5.6 Conflict Handling（矛盾時の処理）

次の場合、実装担当 AI は独自に解消してはならない。

- 確定仕様と本文が矛盾する
- 確定仕様と未決事項が重複する
- 未決事項と却下仕様が重複する
- 指示書と正本が矛盾する
- 複数の正本が存在する
- 既存実装が確定仕様と異なる

必ず編集を停止し、矛盾箇所を報告する。

## 6. Standard Document Adoption Gate（標準文書導入ゲート）

新規リポジトリまたは標準未導入リポジトリでは、設計、仕様変更、実装、commit、push、deploy を開始する前に、中央標準の Canonical Source を定義済み Distribution Mapping に従ってリポジトリ直下へ配置しなければならない。

共通Governanceに加え、Repository Purpose に応じた Document Profile を適用する。

Purpose の確定権限はUser（Takashi Oikawa）にある。AI および installer は Repository 内容から Purpose を推測してはならない。

installer の `--purpose` は `docs/CLASSIFICATION_RULE.md` の Purpose 5値と整合する。

```text
LEARNING
→ LEARNING Profile

GOVERNANCE
DISTRIBUTION
DEVELOPMENT
EXPERIMENT
→ 現行 Profile

未指定
→ 後方互換のため現行 Profile

5値以外
→ invalid、exit 1
```

今回定義する Document Profile は LEARNING のみである。DEVELOPMENT / GOVERNANCE / DISTRIBUTION / EXPERIMENT の必須文書・運用は変更しない。

### 6.0 LEARNING Document Profile（LEARNING文書プロファイル）

Purpose = LEARNING の Repository では、DEVELOPMENT 向け `docs/design` 7文書を必須としない。

Required（必須）:

- `/README.md`
- `/CONSTITUTION.md`
- `/AGENTS.md`

Standard（標準）:

- `/project-notes/CURRENT.md`

Optional（任意）:

- `/project-notes/DECISIONS.md`

重要な Decision を継続管理する必要がある Repository のみ配置する。既に存在する `DECISIONS.md` は削除しない。

Not Required（必須ではない）:

```text
/CHANGELOG.md
/docs/design/README.md
/docs/design/01_REQUEST_DEFINITION.md
/docs/design/02_REQUIREMENTS_DEFINITION.md
/docs/design/03_DATA_AND_SECURITY_DESIGN.md
/docs/design/04_UI_AND_FLOW_DESIGN.md
/docs/design/05_ARCHITECTURE_DESIGN.md
/docs/design/06_OPERATION_AND_HANDOFF.md
/scripts/validate-docs.py
/.github/workflows/validate-docs.yml
```

教材そのものの Markdown・directory 構成は Repository 用途に応じて自由に作成できる。「LEARNING は 4 ファイルしか置けない」という意味ではない。

`CURRENT.md` は作業の現在地点・次作業・Blocker を管理する。LEARNING における標準運用文書であり、D-013 の必須Governance文書10へ追加するものではない。D-016（CURRENT.md 標準採用）の未登録 Decision および未完了作業を上書き・再定義しない。

LEARNING Initial Introduction Unit（LEARNINGの初回導入単位）:

```text
/CONSTITUTION.md
/AGENTS.md
/project-notes/CURRENT.md
```

`/README.md` は必須Governance文書であるが Repository 固有入口であり、installer は作成・上書きしない。`--purpose LEARNING` ではコピー開始前に `/README.md` の存在を確認する。PRESENT なら Preflight を継続する。ABSENT なら何も変更せず停止し、exit 3 とする。Post-copy でも `/README.md` の存在を確認する。installer は README 本文を編集しない。既に存在する CHANGELOG / `docs/design` / validator / workflow は自動削除しない。既存 LEARNING Repository への一括 Migration は行わない。

LEARNING では、必須Governance文書（README / CONSTITUTION / AGENTS）のうち 1 文書でも不足している場合、設計、仕様変更、実装、commit、push、deploy を開始してはならない。`docs/design` 7文書、CHANGELOG、Validation Assets の不存在を LEARNING の導入ゲート違反としてはならない。

LEARNING New Repository Creation Path（LEARNING新規Repository作成経路）:

```text
Purpose != LEARNING
→ 現行 project-bootstrap 運用を維持する

Purpose = LEARNING
→ project-bootstrap の Use this template は使用しない
→ /README.md を持つ Repository を用意する
→ install-project-standards.sh --purpose LEARNING
```

LEARNING 用の別 Template Repository は新設しない。`project-bootstrap` の DEVELOPMENT 向け既存資産は削除しない。

### 6.0.1 Current Profiles including DEVELOPMENT（DEVELOPMENT等の現行プロファイル）

DEVELOPMENT / GOVERNANCE / DISTRIBUTION / EXPERIMENT では、現行の必須Governance文書10 と必須Governance検証資産2 を維持する。

必須Governance文書は次の 10 文書とする。

Central Managed Copies（中央管理コピー） 2:

- `/CONSTITUTION.md`
- `/AGENTS.md`

Repository-Specific Documents（Repository固有文書） 8:

- `/CHANGELOG.md`
- `/docs/design/README.md`
- `/docs/design/01_REQUEST_DEFINITION.md`
- `/docs/design/02_REQUIREMENTS_DEFINITION.md`
- `/docs/design/03_DATA_AND_SECURITY_DESIGN.md`
- `/docs/design/04_UI_AND_FLOW_DESIGN.md`
- `/docs/design/05_ARCHITECTURE_DESIGN.md`
- `/docs/design/06_OPERATION_AND_HANDOFF.md`

Governance検証資産は必須Governance文書に含めない。別分類とする。DEVELOPMENT 等の現行 Profile では必須とする。LEARNING では必須としない。

```text
Governance適用Repository
├─ 必須Governance文書10
└─ 必須Governance検証資産2
   ├─ /scripts/validate-docs.py
   └─ /.github/workflows/validate-docs.yml
```

必須Governance文書10のうち 1 文書でも不足している場合、設計、仕様変更、実装、commit、push、deploy を開始してはならない。
必須Governance検証資産2のうち 1 件でも不足している場合も、Governance適用状態としては未完了であり、設計、仕様変更、実装、commit、push、deploy を開始してはならない。

初回導入時に既存ファイルを上書きしてはならない。

ファイルごとの配置先を判断してはならない。

定義済み Distribution Mapping に従って配置する。`AGENTS_SOURCE.md` は `/AGENTS.md` として配布する。`CHANGELOG_TEMPLATE.md` は通常の新規導入時のみ `/CHANGELOG.md` として配布する。`scripts/validate-docs.py` と `.github/workflows/validate-docs.yml` は Runtime 同パスへ配布する。中央 Canonical Source のファイル名を、判断で配布先へ持ち越してはならない。

初回未導入 Repository では `install-project-standards.sh` が次を一導入単位として扱う。

```text
必須Governance文書10
+
validator
+
workflow
```

### 6.1 Initial Introduction Preflight（初回導入事前確認）

本項は LEARNING を除く現行 Profile に適用する。LEARNING Preflight は §6.0 を正とする。

コピー前にすべて判定する。Governance 9 文書をコピーした後に CHANGELOG または Validation Assets を判定してはならない。部分導入を発生させない。

判定順序を固定する。

```text
Preflight
│
├─ 1. 既存Governance 9文書のいずれかが存在
│    → 何も変更せず停止
│
└─ 既存Governance 9文書なし
     ↓
   2. /CHANGELOG.md確認
     │
     ├─ 不存在
     │    → 通常導入の候補
     │
     └─ 存在
          → 何も変更せず停止
          → Migration承認を要求
     ↓
   3. Validation Assets確認
     │
     ├─ validator または workflow が1件でも存在
     │    → 何も変更せず停止
     │
     └─ 両方とも不存在
          → 全条件PASS後のみコピー開始
```

通常実行で既存 `/CHANGELOG.md` を検出した場合は必ず停止する。installer は既存 CHANGELOG の意味を判定しない。Validation Assets が 1 件でも既存なら無変更停止する。

### 6.2 Rerun after Existing CHANGELOG Approval（既存CHANGELOG承認後の再実行）

本項は LEARNING を除く現行 Profile に適用する。LEARNING Preflight は §6.0 を正とする。

Migration承認後のみ、既存 `/CHANGELOG.md` をUserが再利用承認済みである明示的再実行経路を使用する。

このモードでも、既存Governance 9文書が 1 件でも存在すれば停止する。Validation Assets の衝突確認もコピー開始前に行う。validator または workflow が 1 件でも存在すれば無変更停止する。

9 文書が存在せず、Validation Assets が不存在で、既存 CHANGELOG のみ存在する場合:

- 既存 CHANGELOG → 上書き禁止、編集禁止
- Governance 9 文書 → コピー
- Validation Assets 2 件 → コピー
- installer は CHANGELOG 本文を編集しない
- 導入前 hash と導入後 hash が一致することを確認する
- `CHANGELOG_TEMPLATE.md` と existing `/CHANGELOG.md` の `cmp` は行わない

通常新規導入時のみ、`CHANGELOG_TEMPLATE.md` と `/CHANGELOG.md` の一致を確認する。

### 6.3 project-bootstrap CHANGELOG Exception（project-bootstrapのCHANGELOG例外）

通常 Repository では `/CHANGELOG.md` は Repository 固有履歴正本である。

`project-bootstrap` は明示的例外とする。`project-bootstrap` の `/CHANGELOG.md` は Distribution Template Artifact であり、`project-bootstrap` 自身の変更履歴正本ではない。

Governance / Distribution Source 側の変更履歴正本は `solacom_main/CHANGELOG.md` とする。

### 6.4 Planned Migration Drift（計画済み移行差分）

中央SSOT更新直後は、中央の `CONSTITUTION.md` / `AGENTS.md` / Governance Validation Assets と既存 Repository の配布コピーに一時的差分が発生する。

これは Planned Migration Drift として扱う。異常Driftとして自動修正・一括更新してはならない。Repository単位Migration完了まで許容する。

Allowed Targets（許容対象）:

```text
CONSTITUTION
AGENTS
Governance Validation Assets
```

`update-ai-governance.sh --all` を中央更新直後に実行してはならない。Validation Assets の一括更新も行ってはならない。

### 6.5 Post-Introduction Updates（初回導入後の更新）

本項は DEVELOPMENT 等の現行 Profile に適用する。LEARNING には `docs/design` 7文書のプロジェクト固有化規則を適用しない。

- `CONSTITUTION.md` と `AGENTS.md` は中央正本から配布される管理コピー
- `/scripts/validate-docs.py` と `/.github/workflows/validate-docs.yml` は中央正本から配布される管理コピーである
- 各リポジトリ側で独自編集しない
- 7 文書は初回導入後にプロジェクト固有の設計正本となる
- `/CHANGELOG.md` は Repository 固有履歴正本である（`project-bootstrap` を除く）
- 既存 7 文書を中央テンプレートで上書きしない
- 既存 CHANGELOG を中央テンプレートで上書きしない
- 機能別仕様書を中央テンプレートで上書きしない
- 中央ルール更新は専用の更新工程で行う
- `CONSTITUTION.md` / `AGENTS.md` の更新は `update-ai-governance.sh` を用いる
- 既導入 Repository への Validation Assets 導入は `migrate-governance-validation.sh` を用いる
- 既導入 Validation Assets の更新は `update-governance-validation.sh` を用いる
- `project-bootstrap` への Validation Assets 同期は `sync-project-bootstrap-validation.sh` を用いる
- 更新時も実差分確認と承認を必須とする

## 7. Pre-Work Checks（作業前確認）

実装担当 AI は作業開始前に次を確認する。

- リポジトリルート、ブランチ、HEAD、`origin/main` の一致
- 未コミット差分の有無と対象外差分への非接触
- Userが明示した Repository Purpose。内容から推測しない
- LEARNING の場合: 必須Governance文書 3 件（README / CONSTITUTION / AGENTS）の存在。`docs/design` 7文書および Validation Assets の不存在を欠落としない
- DEVELOPMENT 等の場合: 必須Governance文書 10 件の存在（初回導入済みか）
- DEVELOPMENT 等の場合: 必須Governance検証資産 2 件の存在（Governance適用済みか）
- 作業対象機能の仕様正本パス
- 承認済み作業指示書の範囲

想定外の状態を検出した場合、独自判断で続行せず停止する。

## 8. Change Control（変更管理）

- 変更は承認済み指示書の範囲に限定する
- 対象外ファイルへ触れない
- 確定仕様・未決事項・却下仕様の分類変更は設計担当の承認後のみ
- 実データ例を全体仕様へ一般化しない
- 仕様書整備では、更新後の該当章全文を提示する

## 9. Verification and Completion Determination（検証と完了判定）

- 作業担当 AI の「完了」「矛盾なし」という自己申告だけでは完了としない
- 実ファイル、実差分、仕様 ID 照合結果で判定する
- `git diff --check` の成功だけでは仕様整合性の証明にならない
- commit 前に設計担当レビューを必須とする
- 確定仕様と未決事項の全件突合を行う
- 1 件でも不一致があれば不合格とする

## 10. Git and Deployment Control（Git・デプロイ統制）

- commit、push、deploy はUserまたは設計担当の明示指示がある場合のみ
- 実装担当 AI は、作業完了を理由に commit してはならない
- force push、hard reset、clean 等の破壊的操作は禁止（明示指示時を除く）
- clasp pull / push / deploy は明示指示がある場合のみ

## 11. Security（セキュリティ）

- 個人情報、秘密情報、認証情報をログ、Git、仕様書へ記録しない
- `.env`、`.clasprc.json`、資格情報ファイルを commit しない
- バックアップ、Drive URL 等の運用情報は、指示書で指定された範囲のみ記載する

## 12. Stop Conditions（停止条件）

次の場合、実装担当 AI は独自判断で続行せず停止する。

1. リポジトリルートが想定と異なる
2. ブランチが `main` ではない
3. HEAD または `origin/main` が想定外
4. 中央 7 文書テンプレートが不足している
5. 原本と配布用コピーに差異がある
6. `project-bootstrap/` の構成を判断で変更する必要がある
7. 対象リポジトリに既存Governance 9 文書の一部が存在する（初回導入時）
8. 通常導入で既存 `/CHANGELOG.md` が存在する（Migration承認前）
9. 初回導入で既存 Validation Assets が 1 件でも存在する
10. 初回導入で上書きが必要になる
11. 部分導入が必要になる
12. 対象外差分へ触れる必要がある
13. 確定・未決・却下の分類変更が必要になる
14. 指定外の未決事項追加が必要になる
15. 指定外の確定仕様追加が必要になる
16. 指定外の却下仕様追加が必要になる
17. 複数の正本が存在する
18. GitHub 正本と GAS 実体の一致を前提にしないと進められない
19. Git 操作または clasp 操作が必要になる
20. 個人情報または秘密情報を記載する必要がある
21. Planned Migration Drift を異常として一括更新しようとしている
22. Repository 内容から Purpose を LEARNING と推測して Profile を切り替えようとしている

Purpose = LEARNING の場合、次を停止条件としない。

- 対象リポジトリに `docs/design` 7文書が存在しない
- `/CHANGELOG.md` が存在しない
- Validation Assets が存在しない

停止時は、該当条件、変更済み範囲、未実施範囲を報告する。

## 13. Response Summarization（応答要約）

### 13.1 Separation of Internal Analysis and Output（内部分析と出力の分離）

- 十分な精読・調査・比較・検証は内部作業として実施する
- 内部作業の全過程をユーザーへ表示しない
- ユーザーへ提示するのは、判断・実行に必要な結果だけとする
- 精読量が多いことを、回答量を増やす理由にしない

### 13.2 Response Types（回答種別）

回答は次の 2 種別のいずれかに分類する。

| Type（種別） | Usage（用途） |
| --- | --- |
| Normal Response（通常回答） | 判断・確認・進捗・説明など、会話上の応答 |
| Deliverable Response（成果物回答） | 完成した文章そのものが依頼結果である応答 |

種別判定と送信前確認の手順は `AGENTS.md` に定める。

### 13.3 Standard Structure of Normal Response（通常回答の標準構造）

通常回答は、原則として次の順序で構成する。

1. 結論
2. 理由の要点
3. 次の 1 ステップ

短い回答では見出しを省略できる。見出しそのものを機械的に必須化しない。

### 13.4 Conditions for Deliverable Response（成果物回答の条件）

次のいずれかに該当する場合は、必要な詳細を含む成果物回答として扱う。

- ユーザーが「全文」「詳細」「完全版」「完全指示書」等を明示した
- 実装担当へ渡す完全指示書
- 設計書、仕様書、移行文書、レビュー報告書
- 省略すると成果物として実行・検証できない
- 完成した文章そのものが依頼結果である

成果物であっても、重複説明や目的に不要な背景説明は含めない。

### 13.5 Prohibited Content in Normal Response（通常回答で禁止する内容）

- 内部の調査手順を順番に説明する
- 全セル、全ファイル、全候補などの網羅一覧を無条件に提示する
- 同じ結論を表現を変えて反復する
- 通常説明と実装担当向け完全指示書を本文内で混在させる
- 長文の末尾に短い要約を追加して済ませる
- 回答量を固定行数・固定文字数だけで判定する
- ユーザーが求めていない全注意事項を列挙する

### 13.6 Conditions for Using Tables（表の使用条件）

表は、次の条件をすべて満たす場合のみ通常回答で使用する。

- 比較対象が複数ある
- 同一の比較軸で整理できる
- 文章より短く理解できる
- 表を使うことで項目数が増えない

単一の結論や 3 項目程度の説明には、原則として箇条書きを使用する。

### 13.7 Progress Reports（進捗報告）

長時間作業時の進捗報告にも要約制約を適用する。

進捗報告に含めるのは次のみとする。

- 現在確認できた重要事項
- ブロッカーの有無
- 次に確認している対象

低レベルな操作履歴、全コマンド、全検索対象は表示しない。

### 13.8 Basic Handling of Violations（違反時の基本処理）

回答が冗長であると判定された場合:

1. 追加説明や弁解を行わない
2. 直前の回答を前提にしない
3. 要約版を最初から再出力する
4. 通常回答の標準構造へ戻す

内容上の誤りがある場合のみ:

1. 「間違いでした」と明示する
2. 未確認だった点を簡潔に示す
3. 修正後の結論を提示する
4. 次の最小 1 ステップを提示する

単なる冗長化では「間違いでした」を使用しない。

### 13.9 Non-Adoption of Fixed Numeric Limits（固定数値による制限の不採用）

最大行数、最大文字数、最大見出し数、最大箇条書き数を一律の上限として採用しない。

Reason（理由）:

- 内容によって必要量が異なる
- 数値上限だけを満たす不自然な圧縮が起きる
- 成果物回答と通常回答を同じ数値で評価できない

回答種別と情報の必要性で判定する。
