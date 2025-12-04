# Application Template Repository

## 1. アプリ用テンプレート（`temp_knowledge_app`）

子リポジトリのひな型として、アプリケーションリポジトリのテンプレートを提供します。  
このテンプレートは、新しいアプリケーションリポジトリを迅速にセットアップするための基本的な構造と設定を含んでいます。

### ディレクトリ構成：

```tree
/
├── .github/
│   └── workflows/
│       └── notify_portal.yml      # [重要] 親へ更新を通知するCI
├── docs/
│   └── index.md                   # アプリケーションのドキュメント表紙
├── src/                           # ソースコード置き場
├── .gitignore
├── amplify.yml                    # Amplifyビルド設定
├── mkdocs.yml                     # MkDocs設定
├── README.md                      # このファイル
└── requirements.txt               # 依存ライブラリ
```

#### 主要ファイルの中身

`.github/workflows/notify_portal.yml`

```yaml
name: Notify Portal
on:
  push:
    branches: [ "main" ]
jobs:
  dispatch:
    runs-on: ubuntu-latest
    steps:
      - name: Dispatch to Portal
        uses: peter-evans/repository-dispatch@v2
        with:
          token: ${{ secrets.PROJECT_REPO_PAT }}
          repository: <ORGANIZATION>/<PORTAL_REPO_NAME> # ★案件作成時に書き換える
          event-type: app-update
          client-payload: '{"app_name": "<APP_NAME>", "remote_url": "https://github.com/${{ github.repository }}.git"}'
```
