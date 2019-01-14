### ファイル更新後の手順
#### 1. localhostで表示を確認
```
$ hugo server -D
```

terminalに出力された行から以下を探し、リンクをブラウザに入力、表示確認。
```
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
```

#### 2. 問題なければbuild
```
$ hugo
```

#### 3. buildしたファイルを、AWS S3にアップロード
```
$ aws s3 sync --exact-timestamps --delete ./public s3://ms8music.com  --profile=ms8music-user
```
※ aws cliの導入、基本的な使い方は下記リンクを参照
https://qiita.com/seyself/items/43426f57c50021ea55f8

#### 4. Githubに更新後のファイルをpush
xxxxに更新内容を記入("Update live contents."等。double quotationで囲む必要あり)
```
$ git add .
$ git commit -m "xxxx"
$ git push origin master
```

---
# 初期設定
### 1. Homebrewのインストール
https://brew.sh/index_ja

### 2. Hugoのインストール
```
$ brwe install hugo
```
https://gohugo.io/getting-started/installing/

### 3. aws cli
```
# awscliインストール
$ brew install awscli

# ms8music.comのs3バケットをlist/read/writeするIAMユーザを登録
$ aws configure --profile=ms8music-user

# テスト
$ aws s3 ls s3://ms8music.com --profile=ms8music-user
```

テストでエラーがなく、下記のような出力があれば設定完了
```
                           PRE categories/
                           PRE css/
                           PRE images/
                           PRE js/
                           PRE pages/
                           PRE plugins/
                           PRE tags/
2019-01-13 23:18:25      24341 index.html
2019-01-13 23:18:26        461 index.xml
2019-01-13 23:18:26        655 sitemap.xml
```
