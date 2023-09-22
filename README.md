# Git チュートリアル

Git チュートリアルへようこそ！ このチュートリアルは、gomadoufu が作成したオリジナルのものです。

Git にまったく、あるいはほとんど触れた事がない人をターゲットにしています。用語の説明はあまり行わず、手を動かすことで体得を目指します。

そのため、このチュートリアルはあなたの疑問のすべてに回答しないかもしれません。このチュートリアルを実施する際は、誰か Git に詳しい人に質問できる環境があるとよいでしょう。あるいは ChatGPT がその代わりになるかもしれません。

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

ssh で GitHub にアクセスできるように、アクセストークンを登録してください。

[アクセスキーの作成](https://docs.github.com/ja/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

[アクセスキーの登録](https://docs.github.com/ja/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

[ssh 接続の確認](https://docs.github.com/ja/authentication/connecting-to-github-with-ssh/testing-your-ssh-connection)

## チュートリアル: 既存のディレクトリを Git 管理する

このリポジトリをクローンします。

```sh
$ git clone https://github.com/gomadoufu/git-tutorial
```

### ステップ 1: 現状を確認する

Git 管理されたディレクトリの、現在の状態を確認しましょう。Git 操作をするときは、折に触れて現状を確認するということを意識しましょう。

ls -a で、ディレクトリ内のファイルを確認します。

```sh
$ ls -a
```

Q1. チュートリアル中、Q と書いてあるところは練習問題です。`ls -a`の結果の中から、git と書かれたファイルを見つけましょう。

git status で、現在のディレクトリの状態をチェックできます。

```sh
$ git status
```

Q2. On branch 〇〇 の 〇〇 にはなんと書かれていますか？

git log で、過去に行われた Git 操作を一覧できます。

```sh
$ git log
```

Q3. Commit とは、ソースコードの変更を保存する事です。このディレクトリで、一番最初に Commit した人は誰ですか？

Q4. 一番最初のコミットは何日の何時に行われましたか？

.git ディレクトリを削除してみましょう。
ちなみに ls -l で、.git がファイルなのかディレクトリなのかわかります。列の最初が "d" ならディレクトリです。

```sh
$ ls -al
```

ディレクトリを削除するには、 -r (recursive) オプションが必要です。-f (force) オプションは強力なので、濫用すべきではありません。(今回は確認をスキップするために用います)

```sh
rm -rf .git
```

Q5. .git ディレクトリ削除後、`git status` や `git log` を試して下さい。結果はどうなりましたか？

Q6. .git とはなんでしょうか。

### ステップ 2: Git 管理を始める

いまいる git-tutorial ディレクトリは、Git 管理を外れてしまいました。

このディレクトリを、Git 管理されていない、開発中のディレクトリだと思って、このディレクトリの Git 管理を始めてみましょう。

git init で、そのディレクトリを Git 管理できます。

```sh
git init
```

Q7. .git が作成されたことを確認してください。

Q8. `git status` と `git log` を実行して、結果を確かめてください。

`git init`した後は、いまディレクトリ内にあるファイルの状態を保存するために、すぐに初回のコミットを行います。

さっそく、記念すべき最初のコミットをしましょう。

```sh
git commit -m "initial commit"
```

Q9. 表示されたメッセージを読みましょう

コミットするには、Git にどのファイルをコミットするか教えてあげる必要があります。

`git add` で教える事ができます。ドット`.`はワイルドカードで、現在の変更を全てまとめて Git に教えます。

```sh
git add .
```

Q10. git status を実行して、結果を確かめてください。

あらためて、コミットしましょう。
-m オプションで、コミットにメッセージをつけられます。必ずつけるようにしましょう。日本語で OK ですが、最初のコミットはよく "initial commit"と書かれます。

```sh
git commit -m "initial commit"
```

Q11. git status を実行して、結果を確かめてください。
Q12. Q10 で実行した結果と見比べてください。

### ステップ 3: GitHub と連携する

さて、ここまでの作業で、自分の PC にある git-tutorial ディレクトリは、無事 Git 管理されています。
ここまで、
はじめに

```sh
git init
```

次に

```sh
git add .
```

最後に

```sh
git commit -m "message"
```

としてきました。今後、変更があるたびに`add`と`commit`を繰り返すことで、あなたの開発の変更が記録されていくことになります。

しかしこれだけでは、複数人での開発には不十分です。なんらかの方法で、手元の PC に保存された変更を、チームのメンバーに共有する必要があります。そのために、この Git 管理されたディレクトリを、GitHub のリポジトリと紐付けます。

はじめに、[新しいリポジトリを作成](https://docs.github.com/ja/repositories/creating-and-managing-repositories/creating-a-new-repository)
してください。

`git remote`コマンドで、ローカルの Git 管理されたファイル群(=ローカルリポジトリ)と、いま作成したリモートリポジトリを、結びつける事ができます。

ローカルリポジトリに、リモートリポジトリを追加します。リポジトリを作成した際に表示される画面を参考に、コマンドを入力してください。

```sh
$ git remote add origin git@...git-tutorial.git
```

```sh
git branch -M main
```

```sh
git push -u origin main
```

これで、あなたの開発が無事、GitHub に反映されました。GitHub 上でも、変更を確認してみましょう。
