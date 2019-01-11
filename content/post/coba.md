---
title: "Nuxt.jsの雛形プロジェクトを作成する | Nuxt.js作業ログ01"
date: 2019-01-11T00:20:00+07:00
draft: false
tags:
  - dhamar
  - blog
  - UX/UI
---

ここ最近、Nuxt.jsと戯れているので、未来の自分のためにも日々の知見をためていこうと思います。まず第1回はcreate-nuxt-appで雛形となるプロジェクトを作成する方法です。執筆時の環境は次の通りです。

$ node -v
v8.14.0
$ npm -v
6.4.1

グローバルにcreate-nuxt-appをインストールする

Nuxt.jsの開発環境を用意する方法はいくつかあるようですが、2018年12月19日現在ではcreate-nuxt-appというツールを使うことが公式で推奨されています。Nuxtの開発チームが用意したツールなのでこれを使うのが良いでしょう。

create-nuxt-appはnpmでインストールできます。コマンドは次の通り。

$ npm install -g create-nuxt-app

-gオプションをつけてグローバルにインストールしました。念の為$ whichコマンドで正常にインストールされているか確認しておきましょう。

$ which create-nuxt-app
/Users/<UserName>/.nvm/versions/node/v8.14.0/bin/create-nuxt-app

このようにパスが表示されればOKです。
プロジェクトを作成する

準備ができたので早速雛形プロジェクトを作っていきます。コマンドは$ create-nuxt-app <プロジェクト名>です。今回は「my-nuxt-project」というプロジェクト名で進めます。

$ create-nuxt-app my-nuxt-project

するとどのような設定でプロジェクトを作成するか質問に答える画面が出てきます。今回は下記の通りにしました。

> Generating Nuxt.js project in /Users/diwao/Documents/GitHub/learning/my-nuxt-project
? Project name my-nuxt-project
? Project description My laudable Nuxt.js project
? Use a custom server framework none
? Use a custom UI framework none
? Choose rendering mode Universal
? Use axios module yes
? Use eslint yes
? Use prettier yes
? Author name Daisuke Iwao
? Choose a package manager yarn
Initialized empty Git repository in /Users/diwao/Documents/my-nuxt-project/.git/
yarn install v1.12.3
info No lockfile found.
[1/4] 🔍  Resolving packages...

〜中略〜

success Saved lockfile.
✨  Done in 153.63s.

  To get started:

    cd my-nuxt-project
    yarn run dev

  To build & start for production:

    cd my-nuxt-project
    yarn run build
    yarn start

インストールが終わったら「To get started.」に書いてある通り、作成したmy-nuxt-projectディレクトリに移動して$ yarn run devを実行。サーバが起動したらlocalhost:3000をブラウザで確認してみましょう。

これで正常にNuxt.jsの初期画面が確認できるかと思いきや、なぜかエラーが発生😫

エラー画像

メッセージをよく見るとindex.vueに余計な改行があるのでそれをトレと言われている模様。index.vueを確認してみると、確かに不要と思われる改行がありました。

<style>

.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

↑のstyleの開始タグ直下ですね。ここを削って保存し直しすと今度はちゃんと初期画面が表示されました🤗

Nuxt.js初期表示

初期状態がエラーってどういうことやねん。と思うわけですがこれはNuxtのせいではなくprettierさんが厳しすぎせいなんですよね。Nuxtに罪はない。prettier、勢いで入れてみたけどちょっと厳格すぎるのでなくても良かったかも。この辺はお好みでどうぞ。

ちなみに初期設定の際に聞かれた質問、基本的には好みで答えていけばいいと思うのですが、「Choose rendering mode」だけはちゃんとわかった上で選んでおいたほうがいいかも。ざっくりいうとSSRが必要ならUniversal、いらないならSPAです。
ファイルを整理する

ひととおりNuxtを動かせるところまできたら、次はプロジェクトを管理しやすい形にディレクトリ構成を変更します。これは「Nuxt.jsビギナーズガイド」に書いてあったやり方で、プロジェクトのコアファイルとそうでない部分を明確にする、lintなどのツールの対象範囲をわかりやすくするといった面で効果的だと思うので真似してやってます。

ディレクトリ構成を下記の通り変更します。appディレクトリを新たに作成し、その中にコアファイルを入れている形です。

my-nuxt-project
├── README.md
├── app
│   ├── assets
│   ├── components
│   ├── layouts
│   ├── middleware
│   ├── node_modules
│   ├── pages
│   ├── plugins
│   ├── static
│   └── store
├── node_modules
├── nuxt.config.js
├── package.json
└── yarn.lock

その後、nuxt.confi.jsを開いてsrcDir: 'app'と追記します。

const pkg = require('./package')

module.exports = {
  mode: 'universal',
  srcDir: 'app',

//〜以下そのまま〜

ここまでできたらあとはmy-nuxt-projectのルートで$ yarnを実行し、諸々インストールが終わったあとに改めて$ yarn run devを実行します。これでディレクトリ構成変更前と同様にNuxt.jsの初期画面が表示できるはずです。