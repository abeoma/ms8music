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
$ aws s3 sync --exact-timestamps --delete ./public s3://ms8music.com
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
