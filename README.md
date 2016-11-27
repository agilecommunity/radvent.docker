# 実行方法

## .env ファイルを作成する

ファイルに記載している環境変数の値をdocker-composeが起動時に読み込み、利用する。

```
RADVENT_DB_USER=foo
RADVENT_DB_PASSWORD=bar
RADVENT_DB=baz
DATABASE_URL=postgresql://foo:bar@localhost/baz
RAILS_SECRET_KEY_BASE=(bundle exec rake secret で生成した値を入れればOK)
```

## DBの初期化

```
docker-compose -f docker-compose.run.yml run app bundle exec rake db:migrate
```

## 実行

```
docker-compose -f docker-compose.run.yml up -d
```

データベースのデータは local のx Docker Volume に保存される。
※ 名称は、 プロジェクト名_db_data になっているはず。