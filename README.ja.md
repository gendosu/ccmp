# CCMP - Claude Code マーケットプレイス

Claude Code用の開発支援プラグイン集。

## 概要

CCMP (Claude Code Marketplace) は、Claude Code向けの生産性向上プラグインを含むモノレポです。日々の開発作業を効率化するスキルやコマンドを提供します。

## 利用可能なプラグイン

### CCCP (Claude Code Command Pack)

テスト駆動開発ワークフロー向けのGit操作スペシャリストスキルとマイクロコミットコマンド。

**機能:**
- 包括的なバージョン管理のためのGit操作スペシャリストスキル
- Lucas Rochaの手法に基づくマイクロコミットコマンド
- テスト駆動変更サイクルのサポート
- Conventional Commitメッセージの自動生成
- 自動化されたコミットワークフローの最適化

**バージョン:** 0.1.0

**ドキュメント:** [plugins/cccp/README.md](./plugins/cccp/README.md)

### awesome-statusline

Claude Code ステータスライン自動設定スキル。

**機能:**
- 1コマンドでのステータスライン自動セットアップ
- ディレクトリ名、Gitブランチ、モデル名、トークン統計の表示
- 既存設定の保護と自動バックアップ
- 冪等性のある操作 - 複数回実行しても安全
- ステータスラインでの豊富な情報表示

**バージョン:** 0.1.0

**ドキュメント:** [plugins/awesome-statusline/README.md](./plugins/awesome-statusline/README.md)

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
