---
theme: black
customTheme : "additional"
enableMenu: true
parallaxBackgroundImage: media/bg-mujina-prodx2.webp
# parallaxBackgroundImage: https://s3.amazonaws.com/hakim-static/reveal-js/reveal-parallax-1.jpg
parallaxBackgroundSize: 3300px 3300px
# parallaxBackgroundSize: 2100px 900px
parallaxBackgroundHorizontal: 150
parallaxBackgroundVertical: 50
---

## リアルタイムサーバーの<br>メトリクス可視化

リアルタイム性が求められるサービスの<br>メトリクス収集・分析・監視ソリューション検討

<div class="fs2rem text-right">
<br> Kusanagi
</div>

---

## メトリクス可視化とは

![grafana dashboard demo](media/grafana-dashboard-demo.png){style="width: 70%;" alt="Image description"}

CPU, メモリ使用量, ネットワークトラフィックなど<br>
サーバーの状態をデータとして収集・可視化

---

## モチベーション

- リアルタイムサーバー = オンラインゲームなどのリアルタイム性が求められるバックエンド{.fs2rem}
- 安定性およびパフォーマンスがシビアに重視される{.fs2rem}
    - サーバーの問題でマッチング・インゲームが開始できないと一瞬でユーザーが離れる{.fs2rem}
    - 同時接続人数等の要件を満たしたとしても、パフォーマンスが悪いと運用費がかさむ{.fs2rem}
- 稼働時だけでなく、開発中もパフォーマンスを可視化しておくことで問題の早期発見・解決につなげたい{.fs2rem}
    - = ローカル環境でのパフォーマンスチューニング{.fs2rem}

--

- 一般的なWebサービスではデファクトスタンダードが存在する<br>-> ElasticSearchやPrometheus + Grafana
- リアルタイムサーバーでは何を採用すべきか？
- **「デファクトはないっすね」**
    - by 某大規模IPタイトルMMOゲームエンジニア{.ls-none .fs2rem}

---

## メトリクス可視化<br>ソリューションの選択肢

--

## Elastic Search (on AWS)
- ECサイトなどでのログ解析ではデファクト
- 堅牢なエコシステム
- マッシブなトラフィックに耐えられるインフラ
- 🤔 ローカル環境での運用は事実上不可能

--

## Prometheus + Grafana

- Prometheus: メトリクス収集
- Grafana: 可視化(ビジュアライゼーション)
- Web全般的にそれなりのデファクト性
- k8sと併用するノウハウも多い（スケール耐性）
- ローカル・dockerでも運用可能
- 🤔 Pull型のデータ蓄積
    - データのタイムスタンプが<br>Prometheusのタイムスタンプに依存する
- 🤔 msecオーダーの解析には見せ方の工夫が必要

--

## Influx DB (時系列DB)<br> + 可視化サービス(Grafana等)
- 愚直で柔軟な構成
- リアルタイム性の高いデータ収集
- ローカル・dockerでも運用可能
- 🤔 高負荷アラートなどは自前での実装が必要
- 🤔 自前でスケーリングの設計が必要

--

## 最終手段: 自前で作る

**やめといたほうがいい** <br>

既存のソリューションを踏まえたうえで<br>欲しい要件がある場合に限る

---

## Push型 / Pull型について

- **Push型** : サーバー側がデータを送信する
    - メトリクスサービスのAPIをアプリが叩く
- **Pull型** : メトリクスサービス側がアプリサーバーのデータを取得しに行く

--

## Pull型: Prometheusの例

- アプリ側に **Prometheus Exporter** プラグインをインストール
    - `/metrics` HTTPエンドポイントが用意される
- Prometheusサーバーが定期的(15s間隔とか)に `/metrics` にアクセスし、メトリクスを取得
- **Prometheusでは、データのタイムスタンプ=アクセス時刻となる**

---

## Grafanaについて

- データ可視化ツールとしてはデファクト
- Prometheus, InfluxDB など多くのデータソースに対応
- 古くから存在するが未だに活発（UIおしゃれ）
- ビジュアライゼーション向けのデータ加工機能が豊富
- 大体欲しい機能はなんでもある。手放しで採用してよし(2024)

---

## 実例の話

---

end
<!-- end -->