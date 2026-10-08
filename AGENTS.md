<!--
STANDARD_ID: SCAO-AI-GOVERNANCE-AGENTS
STANDARD_VERSION: 1.5
SOURCE: solacom_main/docs/standards/project-bootstrap/AGENTS_SOURCE.md
DISTRIBUTION_MODE: COPY_FROM_CENTRAL_SSOT
LOCAL_EDIT_POLICY: PROHIBITED
-->

# Agent Operating Procedures（エージェント運用手順）

<!-- Document Info（文書情報） -->
| Item（項目） | Value（値） |
|---|---|
| Document ID（文書ID） | SCAO-AI-GOVERNANCE-AGENTS |
| Version（バージョン） | 1.5 |
| Status（ステータス） | Approved |
| Created Date（作成日） | 2026-09-10 |
| Last Updated（最終更新日） | 2026-10-08 |
| Owner（管理者） | Takashi Oikawa |
| Related Documents（関連文書） | CONSTITUTION.md / ../DOCUMENT_GOVERNANCE_STANDARD.md / project-notes/CURRENT_TEMPLATE.md |

## Repository Purpose（リポジトリ目的）

Purpose の確定権限はUser（Takashi Oikawa）にある。AI は Repository 内容から Purpose を推測しない。

Userが Purpose = LEARNING と明示した場合のみ、LEARNING Profile を適用する。

Userが LEARNING と明示していない場合は、DEVELOPMENT 等の現行 Profile を維持する。GOVERNANCE / DISTRIBUTION / EXPERIMENT の Document Profile 再設計は行わない。

## CURRENT.md Reading Rule（CURRENT.md読込規則）

本節は全 Profile 共通である。Purpose 別 Required Reading Order より前に適用する。

`/project-notes/CURRENT.md` が存在する場合、Purpose 別 Required Reading Order より前に読む。

`/project-notes/CURRENT.md` が存在しない場合は読まない。不存在だけを理由に停止しない。必須Governance文書の欠落として扱わない。

`CURRENT.md` を読んだ場合、作業開始前に次の実状態と照合する。

```text
git status
HEAD
最新commit
```

`CURRENT.md` と実状態が一致する場合、作業を継続する。

`CURRENT.md` と実状態が不一致の場合、`CURRENT.md` を正として扱わない。作業を停止し、不整合内容を報告する。

本規則は必須Governance文書の停止条件追加ではない。CURRENT 存在時の AI 運用規則である。

## CURRENT.md Update Rule（CURRENT.md更新規則）

本節は全 Profile 共通である。

作業終了時は、次を実状態へ更新してから完了報告する。

```text
Completed
Current
Next
Blockers
```

Evidence なしに作業を Completed へ移動しない。

## DECISIONS.md Reading Rule（DECISIONS.md読込規則）

本節は全 Profile 共通である。

`DECISIONS.md` は必須Governance文書へ追加しない。無条件で全文を読まない。

次の場合のみ、必要な Decision を読む。

```text
1. CURRENT.md の Related Decisions に Decision 番号がある
2. Userが Decision 番号を指定した
3. 構成・運用方針・Distribution方式の変更を検討する
```

該当しない場合は読込不要。

LEARNING における意味は、存在し、かつ必要時のみ読むこと、および全文を無条件に読まないことである。読込要否の判定は本節の共通規則に従う。

## Required Reading Order（必読順）

### LEARNING

Userが Purpose = LEARNING と明示した場合、作業開始前に次の順番で読む。

1. `/CONSTITUTION.md`
2. `/README.md`
3. `/project-notes/DECISIONS.md`（共通規則に該当する場合のみ）
4. 今回対象の教材文書

存在しない `docs/design/*` を理由に停止しない。
`/CHANGELOG.md`、`/scripts/validate-docs.py`、`/.github/workflows/validate-docs.yml` の不存在を理由に停止しない。

### DEVELOPMENT and Others（DEVELOPMENT等）

Userが LEARNING と明示していない場合、作業開始前に次の順番で読む。

1. `/CONSTITUTION.md`
2. `/docs/design/README.md`
3. `/docs/design/01_REQUEST_DEFINITION.md`
4. `/docs/design/02_REQUIREMENTS_DEFINITION.md`
5. `/docs/design/03_DATA_AND_SECURITY_DESIGN.md`
6. `/docs/design/04_UI_AND_FLOW_DESIGN.md`
7. `/docs/design/05_ARCHITECTURE_DESIGN.md`
8. `/docs/design/06_OPERATION_AND_HANDOFF.md`
9. 作業対象機能の仕様正本
10. 今回の承認済み作業指示書
11. 関連コード
12. 関連テスト

存在しない文書がある場合、標準導入ゲート違反として停止する。

## Required Governance Document Presence Check（必須Governance文書の存在確認）

### LEARNING

Userが Purpose = LEARNING と明示した場合、作業開始前に次の必須Governance文書の存在を確認する。

```text
/README.md
/CONSTITUTION.md
/AGENTS.md
```

1 件でも不足している場合は停止する。

`/project-notes/CURRENT.md` は標準運用文書である。不存在を必須Governance欠落として停止しない。
`docs/design` 7文書、CHANGELOG、Validation Assets の不存在を停止理由にしない。

### DEVELOPMENT and Others（DEVELOPMENT等）

Userが LEARNING と明示していない場合、作業開始前に、必須Governance文書 10 件の存在を確認する。

```text
/CONSTITUTION.md
/AGENTS.md
/CHANGELOG.md
/docs/design/README.md
/docs/design/01_REQUEST_DEFINITION.md
/docs/design/02_REQUIREMENTS_DEFINITION.md
/docs/design/03_DATA_AND_SECURITY_DESIGN.md
/docs/design/04_UI_AND_FLOW_DESIGN.md
/docs/design/05_ARCHITECTURE_DESIGN.md
/docs/design/06_OPERATION_AND_HANDOFF.md
```

1 件でも不足している場合は停止する。

CHANGELOG 本文を全作業で読む必要はない。
CHANGELOG を Required Reading Order へ無条件追加しない。

## Checks when Changing Managed Markdown（管理対象Markdown変更時の確認）

以下を変更する場合:

- Content（内容）
- Version（バージョン）
- Status（ステータス）
- Last Updated（最終更新日）

編集前に次を確認する。

- Target Document Version（対象文書Version）
- Target Document Last Updated（対象文書Last Updated）
- Required Git History（必要なGit履歴）

DEVELOPMENT 等では、加えて `/CHANGELOG.md` を確認する。
LEARNING では、`/CHANGELOG.md` が存在する場合のみ確認する。不存在を停止理由にしない。

## Document Precedence（文書優先順位）

```text
Latest Explicit User Instruction（ユーザーの最新明示指示）
→ CONSTITUTION.md
→ Project-specific Confirmed Specification（プロジェクト固有の確定仕様）
→ Target Feature Specification Source（対象機能の仕様正本）
→ Approved Work Instruction（承認済み作業指示書）
→ Existing Implementation（既存実装）
→ Comments and Supporting Materials（コメント・補助資料）
```

文書間に矛盾がある場合、実装担当 AI が独自に優先順位を適用して変更してはならない。

矛盾箇所を報告し停止する。

## Two-Phase Procedure for Specification Editing（仕様書編集の2段階手順）

本手順は、F/O/R 台帳で管理する仕様書を編集する場合に適用する。LEARNING 教材編集で F/O/R 台帳が存在しない場合、台帳不存在を導入ゲート違反として停止しない。

### Phase A: Pre-Analysis（事前分析）

- ファイルを変更しない
- F/O/R 台帳を確認する
- 変更予定一覧を作成する
- 各変更の対象 ID を示す
- 分類変更の有無を示す
- 指定外論点の有無を示す
- 設計担当の承認前に編集しない

Report Format（報告形式）:

```markdown
| ID（識別子） | Current Location（現在の位置） | Planned Location（変更予定位置） | Classification Change（分類変更） | Content Change（内容変更） | Result（判定） |
|---|---|---|---|---|---|
```

### Phase B: Editing（編集）

- 承認済み一覧にある変更だけを実施する
- 承認一覧にない変更を行わない
- 新規 F/O/R-ID を追加しない
- 分類を変更しない
- 独自の整理、一般化、再設計を行わない
- 追加変更が必要になった場合は停止する

## Required Checks after Editing（編集後の必須検査）

### FROZEN

各 F-ID について次を確認する。

- 確定仕様台帳に存在する
- 状態が `FROZEN`
- 本文の確定仕様として存在する
- 未決事項に存在しない
- 却下仕様に存在しない
- 意味変更がない

### OPEN

各 O-ID について次を確認する。

- 未決事項台帳に存在する
- 状態が `OPEN`
- 確定仕様に存在しない
- 却下仕様に存在しない
- 未登録の OPEN 項目がない

### REJECTED

各 R-ID について次を確認する。

- 却下仕様台帳に存在する
- 状態が `REJECTED`
- 有効仕様として存在しない
- 却下理由が維持されている

## Pre-commit Review（commit前レビュー）

- 実装完了を理由に、実装担当 AI が自動的に commit / push してはならない
- commit / push は、Userまたは設計担当から明示指示がある場合のみ実施できる
- 明示指示前に、設計担当による git diff、F/O/R照合、対象外差分非接触のレビューを必須とする
- レビューで1件でもFAILがある場合はcommit不可

## Response Generation and Pre-Send Gates（応答生成と送信前ゲート）

規範は `CONSTITUTION.md` §13 に従う。回答生成後、送信前に次を順番に判定する。

### Gate 1: Response Type（回答種別）

次のどちらかを判定する。

```text
NORMAL_RESPONSE
DELIVERABLE_RESPONSE
```

成果物回答の条件は `CONSTITUTION.md` §13.4 に従う。

### Gate 2: Normal Response Check（通常回答チェック）

`NORMAL_RESPONSE` の場合、以下をすべて確認する。

- 冒頭で結論が理解できる
- 理由は判断に必要な要点へ限定されている
- 次の行動は原則 1 つである
- 内部調査過程を表示していない
- 網羅一覧を無条件に表示していない
- 成果物本文を混在させていない
- 同じ内容を繰り返していない
- 表が文章より簡潔である（表を使用した場合）
- ユーザーが求めていない背景説明を含めていない

1 項目でも不合格なら、回答を削るのではなく、通常回答として再構成する。

### Gate 3: Deliverable Response Check（成果物回答チェック）

`DELIVERABLE_RESPONSE` の場合、以下を確認する。

- 成果物として必要な情報が欠落していない
- 対象範囲が明確である
- 不要な会話説明が成果物へ混入していない
- 同じ指示が複数箇所で重複していない
- ユーザー向け要約と成果物本文が区別されている

### Gate 4: Regeneration（再出力）

ゲート不合格時は、`CONSTITUTION.md` §13.8 に従い、説明を追記せず回答全体を再生成する。

冗長化違反と内容上の誤りを混同しない。誤り訂正時のみ「間違いでした」を使用する。
