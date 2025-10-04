# DockerManagerDemo
Dockerを管理するソフトのデモ環境

## 環境紹介

- targetWordpress/
    - 監視対象としての Wordpress
- watcherDockge/
    - Dockge による監視の検証
    - ◆◆注意◆◆
        - Dockgeでスタックを削除するとフォルダごと消される(≠ 管理画面上のみの削除ではない)
- watcherPortainer/
    - Portainer による監視の検証

## 環境構築

1. 各環境にて、`docker compose up -d`
    - `-d` でデーモン化

