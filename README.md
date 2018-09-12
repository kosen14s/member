# kosen14s #profile

https://kosen14s.github.io/member/

kosen14sのメンバーを紹介するサイトです。  
今まで `#profile` チャンネルに自己紹介を書いていましたが、過去ログとなっていつか消えてしまうことや、単純に見にくいという問題点を解決するために作ったものです。  

> Nuxt.js project

# メンバーの追加

メンバーページに自己紹介を追加するには2つの方法があります。

1. 14sメンバーに、全部のデータを渡してまかせる。
2. 14sGitHubのメンバーになって自分で変更する。

できれば自分でやってもらえると嬉しい。GitHubのアカウントがある人は、メンバーになっておいて損はなさそう。とりあえず、`#profile` チャンネルでGitHubのアカウント叫んでくれれば誰かが対応します。メンバーになったら、以下に解説する手順でデータ更新ができます。

対応する側のメンバーは、ココ↓の `Invite member` を押してアカウント名入力すればメンバーに追加できる。  
https://github.com/orgs/kosen14s/people 

## 1. アイコン画像をアップロード
### 1-1. `icons` フォルダをクリック
![](https://imgur.com/OjQAZlQ.png)

### 1-2. `Upload files` をクリック  
![](https://imgur.com/vPPzQ3R.png)

### 1-3. 画像をドラッグアンドドロップ（ファイル名を自分の名前(英字)にしておくと良い）して各項目を入力。ボタン押して終わり。  
![](https://imgur.com/eAMyrnp.png)

## 2. 自己紹介を記述
### 2-1. `member.json` をクリック  
![](https://imgur.com/fDoN7Ll.png)

### 2-2. 鉛筆アイコンをクリック  
![](https://imgur.com/J2bpizm.png)

### 2-3. テンプレに従って情報を入力。テンプレについては下で詳しく。

### 2-4. `Create a new branch for this commit...` に変更。  
![](https://imgur.com/BaMLhbZ.png)

### 2-5. Commit changes を入力してボタンを押す。

### 2-6. Create pull request を押す。  
![](https://imgur.com/vEbJQK6.png)

### 2-7. Slackで「pull request 投げました」と報告。

## テンプレについて

- 書きたくない内容は、""を付けず `null` と書くことで非表示にできます。
- 各種SNSのidは、下記の *** の部分に自動で入るのでフルパスを書かないでください。
- `channels` にはお気に入りのチャンネルや、良く出没するチャンネルを書いておくと、新規加入者がどんなチャンネルがあるのかわかってよいです。
- JSONは、次のオブジェクトがある場合は `,` をデータの末尾につけなきゃいけないのでお忘れなく。

```
{
  "name":   "自分の名前（ペンネーム）を入力",
  "icon":   "先ほどUploadしたアイコン画像のファイル名を入力",
  "origin": "どこの学校か",
  "area":   "活動範囲でもいいし住んでる県でもいい",
  "links": {
    "site_url":     "自分のサイトなどのフルパスを記述",
    "twitter_id":   "Idを@なしで記述 [https://twitter.com/***]",
    "facebook_id":  "Idを記述 [https://www.facebook.com/***]",
    "instagram_id": "Idを記述 [https://www.instagram.com/***]",
    "github_id":    "Idを記述 [https://github.com/***]",
    "tumblr_id":    "Idを記述 [https://***.tumblr.com/]",
    "blog_url":     "自分のブログのフルパスを記述",
    "youtube_url":  "自分のチャンネルのフルパスを記述"
  },
  "channels": [
    "design","video","frontend","font","emoji","virtial-youtuber"
  ],
  "self_introduction": [
    "自由記述自己紹介文の１段落目です。これは１段落目の文章です。",
    "改行したいときは、こうやります。改行された２段落目です。",
    "３段落目です。最後の段落以外に,を付けるのを忘れずに"
  ]
},
```

# Build Setup

``` bash
# install dependencies
$ npm install # Or yarn install

# serve with hot reload at localhost:3000
$ npm run dev

# build for production and launch server
$ npm run build
$ npm start

# generate static project
$ npm run generate
```

For detailed explanation on how things work, checkout the [Nuxt.js docs](https://github.com/nuxt/nuxt.js).

