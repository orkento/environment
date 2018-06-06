# Subversion設定手順(MSYS2)

## インストールアプリ

- msys2

## 構築手順

クライアントマシンにmsys2でsubversionをインストール

## クライアント証明書の設定

`~/.subversion/servers`に以下の設定を追加

```
[global]
ssl-client-cert-file = 証明書ファイルの絶対パス
ssl-client-cert-password = 証明書のパスワード
```

## svn diffのカラー設定

`~/.subversion/config`に以下の設定を追加

```
[helpers]
diff-cmd = colordiff
```

## コマンドメモ

- `svn diff -r PREV:HEAD` ...1つ前の差分
