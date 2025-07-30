# docker-deploy


このリポジトリは、フロントエンドとバックエンドを本番環境にデプロイするための設定を提供します。
各コンポーネントは git submodule として管理されており、Docker Compose を使用して統合された本番環境を構築します。

## ディレクトリ構成

```
.
├── frontend/         # フロントエンド（git submodule）
├── backend/          # バックエンド（git submodule）
├── nginx/
│   ├── certs/        # SSL証明書 (server.cert.pem, server.key.pem)
│   └── default.conf  # nginx の設定ファイル
└── compose.yml
```

## セットアップ

```
$ git clone --recurse-submodules https://github.com/trans-itf/docker-deploy.git
$ git submodule update --init --recursive
```


## SSL証明書の設定

`nginx/certs/`に以下のファイルを配置してください。

- `server.cert.pem`: SSL証明書
- `server.key.pem`: SSL秘密鍵
- `root_plus_intermediates.cert.pem`: 中間証明書とルート証明書を結合したファイル


## backendの環境変数・GCPのkeyの設定
Dockerfile.backendと同じ階層に、以下2つのファイルを配置してください。
- key.json
  - Google Cloud の認証情報ファイル
- .env(OPENAI_API_KEY=<APIキー> と記載)  


## 🐳 Docker を使用した本番環境の構築

```
$ docker compose build
$ docker compose up -d
```
