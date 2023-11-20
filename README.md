# 簡単な手順書
①イメージがプッシュされたリポジトリの用意
作成したECRのリポジトリにあるプッシュコマンドを参考に、ビルドしたイメージをプッシュする（ログイン→タグ付け→イメージのプッシュ）
※ビルド時は以下のコマンドを実行する
```
docker build -f ./docker/laravel/Dockerfile . --platform linux/amd64
```
②

参考：https://zenn.dev/imah/articles/5d761f8f8c26fe