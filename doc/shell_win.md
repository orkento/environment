# シェル環境構築手順(Windows)
## インストールアプリ

- cmdermini
- msys2
- git bash(git for windows?)

## 構築手順

1. アプリインストール
2. 環境変数でHOME=C:\Users\ユーザー名を設定する
3. msys起動させ以下のコマンドでパッケージを最新にする

  ```
  pacman -Syu
  (処理が中断するためshellを終了させる)
  pacman -Syu
  pacman -Su
  ```

4. cmdより```mklink /d```コマンドで以下のシンボリックリンクを作成(.ssh/configが読み出せないため)
  - シンボル名...msys64\home\ユーザー名
  - リンク先...C:\Users\ユーザー名
5. cmder.exeをC:\ProgramData\Microsoft\Windows\Start Menu\Programsに登録
6. cmderを起動しSettingにてインストール済みのBashを読み込ませる
7. msysをデフォルトのタスクにする
8. .bashrcに/c/ProgramData/chocolatey/binのパスを追加(Emacsアプリ用)

***msys64/usr/bin/をパスに追加するとgit bashの一部のコマンドが利用できなくなる***

### msysの必須パッケージ

- git
- openssh
- fish
- markdown

## fishシェル

### インストールfisherman

```
curl -Lo ~/.config/fish/functions/fisher.fish --create-dirs https://git.io/fisher
```

***oh-my-fishは古いため非推奨***

### 推奨テーマ

cmderにてほとんどのテーマの表示が乱れるため以下を推奨

- フォント...Anonymice Powerline([フォント一覧](https://github.com/powerline/fonts))
- テーマ...omf/theme-fox

