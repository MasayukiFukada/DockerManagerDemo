# DockerManagerDemo

Dockerを WebUI で管理するソフトのデモ環境

- 総括
    - Docker 専用のホストが1台だけで、 CPU などの監視を行わないのであれば Dockge で十分
        - CPU なども気にかけるのであれば Portainer
    - Docker を走らせるホストが複数台あるのであれば、Portainer の Agent を動かして本体の方もどこかで動かす

## 環境紹介

- targetWordpress/
    - 監視対象としてのダミー Wordpress

- watcherDockge/
    - Dockge による監視の検証
        - 複数の compose.yaml をシンプルに管理できる
            - 単純にコンテナの上げ下げと、compose.yaml の記述サポート
        - ディレクトリの`制限あり`
            - Dockge の管理ディレクトリ配下の浅い階層に置かないと認識しないので注意
            - プロジェクトディレクトリのcompose.yamlに張ったシンボリックリンクでの管理も NG
    - ◆◆注意◆◆
        - Dockgeでスタックを削除するとディレクトリごと消される(≠ 管理画面上のみの削除ではない)
        - Dockgeで管理したいcomposeはDockgeの管理ディレクトリ配下の階層が深くなるとダメ
```
- <管理ディレクトリ>
    - 対象ディレクトリ
        - ○: compose.yaml
        - さらにもう一階層
            - ×: compose.yaml
```
- watcherPortainer/
    - Portainer による監視の検証
        - Docker ホストの管理
            - CPU、メモリの使用量などを確認するダッシュボードあり
        - 今回は Agent コンテナも使用しているが、 Agent 無しで直接ホストの管理もできる
            - ホストが一台の場合に有効
            - Agent を使うと WebUI を1箇所にして複数の Docker ホスト管理が可能
        - ディレクトリの`制限無し`
    - 今回はAgentも同じように起動するように設定している
        - EnvironmentでAgentを追加する場合は、`agent:9001` で追加できるハズ

## 環境構築

1. 各環境にて、`docker compose up -d`
    - `-d` でデーモン化

## 検証

1. Dockge( [http://localhost:5001](http://localhost:5001) )か、Portainer( [http://localhost:9000](http://localhost:9000) )を確認する
    - 操作性や機能

