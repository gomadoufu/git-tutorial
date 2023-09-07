# Git チュートリアル

Git チュートリアルへようこそ！ このチュートリアルは、gomadoufu が作成したオリジナルのものです。
Git にまったく、あるいはほとんど触れた事がない人をターゲットにしています。用語の説明は全く行わず、手を動かすことで体得

さっそくはじめましょう。

## ツールのインストール

### Linux

パッケージ管理ツールでインストールできます。ディストリビューションに応じてツールを選択してください。

```sh
# Redhat系
$ sudo yum install git
# Debian系
$ sudo apt install git
```

### Mac

Homebrew でインストールするのが一般的です。

```sh
$ brew install git
```

### Windows

[git インストーラ](https://gitforwindows.org/)でインストールできますが、WSL の使用をお勧めします。

## Git 初期設定

### ツールの確認

```sh
$ git --version
git version 2.42.0
```

### 設定

```sh
git config --global user.name "your-name"
git config --global user.email "example@gmail.com"
```

## チュートリアル 1: 既存のディレクトリを Git 管理する

このリポジトリをクローンします。

```sh
$ git clone https://github.com/gomadoufu/git-tutorial
```

### ステップ 1: 現状を確認する

Git 管理されたディレクトリの、現在の状態を確認しましょう。これは非常に重要な事です。

ls -a で、ディレクトリ内のファイルを確認します。

```sh
$ ls -a
```

Q1. git と書かれたファイルを見つけましょう。

git status で、現在のディレクトリの状態をチェックできます。

```sh
$ git status
```

Q2. On branch 〇〇 の 〇〇 には何が入っていますか？

git log で、過去に行われた Git 操作を一覧できます。

```sh
$ git log
```

Q3. Commit とは、ソースコードの変更を保存する事です。このディレクトリで、一番最初に Commit した人は誰ですか？

Q4. 一番最初のコミットは何日の何時に行われましたか？

.git ディレクトリを削除してみましょう。
ちなみに ls -l で、.git がファイルなのかディレクトリなのかわかります。列の最初が "d" ならディレクトリです。

```sh
$ ls -l
```

ディレクトリを削除するには、 -r (recursive) オプションが必要です。

```sh
rm -rf .git
```

Q5. .git ディレクトリ削除後、`git status` や `git log` を試して下さい。結果はどうなりましたか？

Q6. .git とはなんでしょうか。