# CCMP - Claude Code マーケットプレイス

Claude Code用の開発支援プラグイン集。

## 概要

CCMP (Claude Code Marketplace) は、Claude Code向けの生産性向上プラグインを含むモノレポです。日々の開発作業を効率化するスキルやコマンドを提供します。

## 利用可能なプラグイン

<table>
<thead>
  <tr>
    <th>プラグイン名</th>
    <th>説明</th>
    <th>種別</th>
    <th>機能名</th>
    <th>バージョン</th>
    <th>ドキュメント</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="7"><strong>CCCP</strong><br>(Claude Code Command Pack)</td>
    <td rowspan="7">テスト駆動開発ワークフロー向けのGit操作スペシャリストエージェントとマイクロコミットコマンド</td>
    <td>Agent</td>
    <td>git-operations-specialist - Git操作全般（コミット、ブランチ、マージ、競合解決）</td>
    <td rowspan="7">0.3.0</td>
    <td rowspan="7"><a href="./plugins/cccp/README.md">README</a></td>
  </tr>
  <tr>
    <td>Agent</td>
    <td>project-manager - プロジェクト管理全般</td>
  </tr>
  <tr>
    <td>Command</td>
    <td>commit - git stageされている内容でコミット</td>
  </tr>
  <tr>
    <td>Command</td>
    <td>micro-commit - コンテキストベースのマイクロコミット分割</td>
  </tr>
  <tr>
    <td>Command</td>
    <td>todo-task-planning - タスク計画実行</td>
  </tr>
  <tr>
    <td>Command</td>
    <td>todo-task-run - TODOファイルからタスク実行してPR作成</td>
  </tr>
  <tr>
    <td>Skill</td>
    <td>key-guidelines - 開発ガイドライン参照</td>
  </tr>
  <tr>
    <td rowspan="1"><strong>awesome-statusline</strong></td>
    <td rowspan="1">Claude Code ステータスライン自動設定スキル</td>
    <td>Skill</td>
    <td>setup-statusline - ステータスライン自動セットアップ</td>
    <td rowspan="1">0.1.0</td>
    <td rowspan="1"><a href="./plugins/awesome-statusline/README.md">README</a></td>
  </tr>
  <tr>
    <td rowspan="1"><strong>codex</strong></td>
    <td rowspan="1">Codex MCP連携プラグイン - コードレビュー、技術調査、ドキュメント生成</td>
    <td>Skill</td>
    <td>codex - コードレビュー、技術調査、ドキュメント生成、カスタムクエリ</td>
    <td rowspan="1">0.1.1</td>
    <td rowspan="1"><a href="./plugins/codex/README.md">README</a></td>
  </tr>
</tbody>
</table>

## インストール

### マーケットプレイスの追加

```bash
/plugin marketplace add gendosu/ccmp
```

### プラグインのインストール

```bash
/plugin install cccp@gendosu-claude-plugins
```

## プラグイン開発

### ディレクトリ構造

```
ccmp/
├── .claude-plugin/
│   └── marketplace.json       # マーケットプレイスマニフェスト
├── plugins/
│   └── cccp/                  # CCCPプラグイン
│       ├── .claude-plugin/
│       │   └── plugin.json
│       ├── skills/
│       ├── commands/
│       ├── README.md
│       └── LICENSE
├── docs/
│   └── memory/                # 調査・計画記録
├── README.md                  # 英語版マーケットプレイス説明
├── README.ja.md               # 日本語版マーケットプレイス説明
├── LICENSE                    # MITライセンス
└── .gitignore
```

### 新しいプラグインの追加

1. `plugins/`配下に新しいディレクトリを作成
2. プラグインのメタデータを含む`.claude-plugin/plugin.json`を追加
3. スキルまたはコマンドを実装
4. `marketplace.json`を更新して新しいプラグインを登録
5. プラグインのREADME.mdにドキュメントを追加

### プラグインの自己完結性（重要）

Claude Codeはプラグインをキャッシュにコピーするため、`../`を使用した相対パス参照はサポートされていません。各プラグインは必要なファイルをすべて含む自己完結型である必要があります。

## バージョン管理

- **マーケットプレイスバージョン:** `marketplace.json`で管理（現在: v1.0.0）
- **個別プラグインバージョン:** 各プラグインエントリ内で管理
- **Gitタグ:** マーケットプレイス全体でバージョン管理

## トラブルシューティング

### プラグインが見つからない

マーケットプレイスが正しく追加されているか確認してください:

```bash
/plugin marketplace list
```

### インストールに失敗する

1. `jq`でmarketplace.jsonの構文を検証:
   ```bash
   jq . .claude-plugin/marketplace.json
   ```

2. プラグインの`plugin.json`が存在するか確認:
   ```bash
   ls plugins/*/.claude-plugin/plugin.json
   ```

### プラグインが読み込まれない

すべての必要なファイルがプラグインディレクトリ内にあり、`../`による外部依存関係がないことを確認してください。

## ライセンス

このプロジェクトはMITライセンスの下でライセンスされています - 詳細は[LICENSE](LICENSE)ファイルを参照してください。

## コントリビューション

コントリビューションを歓迎します！お気軽にPull Requestを提出してください。

## 作者

**Gendosu**

## リポジトリ

[https://github.com/gendosu/ccmp](https://github.com/gendosu/ccmp)
