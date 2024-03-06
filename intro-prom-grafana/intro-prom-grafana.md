---
theme: black
enableMenu: true
# parallaxBackgroundImage: https://s3.amazonaws.com/hakim-static/reveal-js/reveal-parallax-1.jpg
# parallaxBackgroundSize: 2100px 900px
# parallaxBackgroundHorizontal: 200
# parallaxBackgroundVertical: 50
---

## Webアプリケーションの<br>メトリクス可視化

`ASP.NET` サーバーに対する<br>Prometheus + Grafana を利用したソリューション

---

## メトリクス可視化とは

---

## モチベーション

---

## メトリクス可視化<br>ソリューションの選択肢

--

## Elastic Search (on AWS)
- 堅牢なエコシステム
- マッシブなインフラストラクチャ
- ローカル環境での運用は事実上不可能

--

## Prometheus + Grafana
- それなりのデファクトスタンダード性
- msecオーダーのパフォーマンス解析には工夫が必要

--

## Influx DB (時系列DB)<br> + 可視化サービス(Grafana等)
- 愚直で柔軟な構成
- リアルタイム性の高いデータ収集
- 高負荷アラートなどのサポートは自前での実装が必要

---

## Prometheus と Grafana <br>について

--

## Prometheus
- 小規模～大規模まで導入可能（スケールへの耐性）
- k8sと連携する場合の事例も多くみられる
- Prometheusの機能

--

## Grafana
- データ可視化ツールとしてはデファクトスタンダード
- 古くから存在するが未だモダンにアップデートされている<br>(競合がKibanaぐらい)

---

## 導入のハードル

- 学習コスト

---

## Prometheusのエコシステム

--

※図

--

## Pull型のデータ蓄積

--

## ASP.NETアプリケーション側の対応

- Prometheus ExporterのNuGetパッケージがある
- `/metrics` エントリポイントを開けるミドルウェアを仕込む

---

## こんな感じ
