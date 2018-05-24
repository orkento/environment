# sshサーバー構築手順(MSYS2)

### 参考サイト

- [How to Get an Unix/Linux Environment on Windows with MSYS2](https://www.booleanworld.com/get-unix-linux-environment-windows-msys2/)
- [SSHの鍵認証設定](https://qiita.com/gotohiro55/items/36a22516de2b381b3c6e)
- [sshd_configの設定項目の理解を目指す](https://unskilled.site/sshd_config%E3%81%AE%E8%A8%AD%E5%AE%9A%E9%A0%85%E7%9B%AE%E3%81%AE%E7%90%86%E8%A7%A3%E3%82%92%E7%9B%AE%E6%8C%87%E3%81%99/)

## インストールアプリ

- msys2


## 構築手順

1. サーバーマシンにmsys2でopensshをインストール
2. 以下のコマンドでhost_keyを作成

```
ssh-keygen -f /etc/ssh/ssh_host_rsa_key -N '' -t rsa
ssh-keygen -f /etc/ssh/ssh_host_dsa_key -N '' -t dsa
ssh-keygen -f /etc/ssh/ssh_host_ecdsa_key -N '' -t ecdsa
ssh-keygen -f /etc/ssh/ssh_host_ed25519_key -N '' -t ed25519
```

3. /etc/ssh/sshd_configの設定を以下のように修正(**※事前にバックアップを取ること**)

```
PasswordAuthentication yes
HostKey /etc/ssh/ssh_host_rsa_key
#HostKey /etc/ssh/ssh_host_dsa_key
HostKey /etc/ssh/ssh_host_ecdsa_key
HostKey /etc/ssh/ssh_host_ed25519_key
```

4. ```/usr/bin/sshd```と指定して起動し別PCから接続できるか確認
4. クライアントPCにてssh鍵の生成
5. クライアント鍵の権限を以下のように変更

```
chmod 600 id_rsa
# Windowsのファイルシステムでは権限を以上の通りに変更できないことがあるため以下のようになる
-rw-r--r-- id_rsa
```

6. id_rsa.pubをサーバーに転送しサーバーPCに移動
7. ~/.ssh/authorized_keysにid_rsa.pubの内容を追加
8. 権限を以下のように変更

```
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
# Windowsのファイルシステムでは権限を以上の通りに変更できないことがあるため以下のようになる
drwxr-xr-x ~/.ssh/
-rw-r--r-- ~/.ssh/authorized_keys
```

9. AuthorizedKeysFileに**絶対パスで**authorized_keysファイルの場所を指定
10. クライアントから```ssh -vT```で接続を確認

## sshd操作コマンド

TODO

## サービス化

### スタートアップへの登録

ショートカットを作成し、リンク先に以下のコマンドを指定して```Windowsキー + R > shell:startup```でスタートアップに登録する

```
%COMSPEC% /c "C:\msys64\usr\bin\sshd.exe"
```
