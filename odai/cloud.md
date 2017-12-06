---
layout: default
title: "クラウド選定基準 in Japan"
image: /icon/ms/cloud.png
permalink: /odai/cloud
lang: ja
name: sre-infra-system.jp
---

<!-- Google Tag Manager -->
<script>(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start':new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0],j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src='https://www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f);})(window,document,'script','dataLayer','GTM-PQV7D3D');</script>
<!-- End Google Tag Manager -->
<!-- Google Tag Manager (noscript) -->
<noscript><iframe src="https://www.googletagmanager.com/ns.html?id=GTM-PQV7D3D" height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
<!-- End Google Tag Manager (noscript) -->

<div id="fb-root"></div>
<script>(function(d, s, id) {
  var js, fjs = d.getElementsByTagName(s)[0];
  if (d.getElementById(id)) return;
  js = d.createElement(s); js.id = id;
  js.src = 'https://connect.facebook.net/ja_JP/sdk.js#xfbml=1&version=v2.11&appId=1374995676111926';
  fjs.parentNode.insertBefore(js, fjs);
}(document, 'script', 'facebook-jssdk'));</script>

# クラウド選定基準 in Japan

## 選定基準 201712版

- 問１：堅実派／チャレンジ派

  あなたのプロジェクトの社風は、

  1. MySQLは心配だからOracleデータベース使う  
  2. MySQLで必要十分

  のどちらですか？

  1の場合 → AWS一択です。  
  2の場合 → GCPが最強です。

- 問２：社内向けシステム／社外向けシステム

  あなたのプロジェクトのサービス内容は、

  1. 社内システム：社員１万人〜
  2. 社内システム：社員50人以下
  3. 社外システム：ECサイト等

  のどちらですか？

  1の場合 → Microsoft Azure でActive Directory 認証使いましょう。  
  2、3の場合 → GCP ＆ g suite (gmail) 認証使いましょう。

- 問３：モノシリック／マイクロサービス

  あなたのプロジェクトは、(phpの場合)
  
  1. SymfonyやLaravelによるモノシリックアプリケーションですか？
  2. lumenやslim3によるマイクロサービスですか？

  1の場合 → AWSが一番使い勝手がよいです。  
  2の場合 → GCP ＆ GAE & GKE 使いましょう。

- 問４：国内派／国外OK派

  あなたのプロジェクトは、
  
  1. データは全部国内必須。
  1. データは海外でもかまわない。

  1の場合 → Microsoft Azureの「東日本リージョン」「西日本リージョン」で冗長化しましょう。  
  2の場合 → GCPの「東京リージョン」「オレゴンリージョン」で冗長化しましょう。同一LAN内のように使えます。

## 何故クラウドが必須なのか

例：画像処理  
　これまで： 投稿記事に写真をuploadします。  
　これから： 投稿記事にuploadされた写真を、アダルト画像判定＆公開可否を判定後登録します。 

といった機能の標準装備が必要です。  
これができなかったのがオンプレ、出来るようになったのがクラウドです。

## クラウドのシェア

[世界のクラウド市場シェアのNo１は？](http://cloudnights.net/cloud/cloud_research/)  
の記事(2017年第2四半期)によると、

||AWS|Microsft<br>Azure|IBM|GCP|Next10|他|
|---|---|---|---|---|---|---|
|2017Q2|34%|11%|8%|5%|19%|23%|
|1年の成長率|+1%|+3%|0%|+1%|-1%|-5%|

- AWS一強
- 今後の成長が見込めるのはAWS,Microsft Azure,GCPの３クラウドのみ

です。

クラウドビジネスは規模＆開発力勝負のビジネスです。何年か後に、

- 「AWSと同じようなサービス提供」のクラウドは生き残り
- 「AWSに満たないサービス提供」のクラウドは無くなる

と思っていてよいです。

## 各クラウド寸評

- AWS

  - No1ブランドです。
  - 一番歴史があります。
  - 既に技術的負債がたくさんあります。(例：EC2ガチャ [AWSバッドノウハウ集 2017/02](https://qiita.com/yayugu/items/de23747b39ed58aeee8a) )
  - 隠れ運用負荷が多いです。
  - 豊富すぎる機能があります。
  - IT系求人サイト上では、AWSオンリーです。
  - オンプレでも、「バックアップ先はS3」「DNS(GSLB)はRoute53」のように一部機能のみ使用される事も多いです。

- Microsoft Azure

  - Windows系システムに一番やさしいクラウドです。
  - 日本に「東日本リージョン」「西日本リージョン」の２つがあり、国内でマルチリージョンが可能です。
  - 自社所有日米間海底ケーブル回線太さは世界で２番めです(一番は米軍)
  - 2016年頃に、いろんな機能が再開発されました。旧機能は技術的負債の塊です。
  - オンラインマニュアルの日本語版に、旧機能の説明が残っている事が多く、「Microsoft Azureを本格活用したいならもう２年待て」感が強いです。
  - ファイルサーバ(cifsマウント)があるのはMicrosoft Azureのみです。

- GCP

  - 一番お財布にやさしいクラウドです。（だいたい他クラウドの7割）
  - 2016-11に、東京リージョンがオープンし、第１選択肢になりました。
  - bigqueryのように、まだ日本に来ていないサービスがあります。
  - 隠れ運用負荷が一番小さいクラウドです。（ハードウェア交換時無停止、オンラインディスク拡張あたり）
  - 機能が少ないため、（オンプレ同様の）自力準備が必要な部分があります。(memcachedとか、NFSサーバとか...)
  - bigqueryだけは他のクラウドでの代替機能が実質存在しない為、AWS使用してても「集計だけはbigquery」を使う場合があります。
  - クラウドの中で、「事前申請なく負荷試験OK」なのはGCPだけです。これ、ネットワーク基盤の実力が、「他のクラウド <<<< (超えられない壁) <<< GCP」という話...

- 他のクラウド

  開発力が上の３社に満たないクラウドは、ニッチ分野でしか生き残れません。

  [Googleの採用担当が明かす、逸材を採用する4つの法則とは「面接は複数で行う」](http://news.livedoor.com/article/detail/10001864/)  
  によると、googleの採用は


  - 年間200万人を超える応募者
  - 1年に数千人採用

  という規模感です。

  このうち、どれくらいの人数が GCP の技術者として働くのかはわかりませんが、  
  国内クラウド業者の「技術者全部で10名」みたいな規模感では太刀打ちできません...

<div class="sns">
  <div>
    <a href="https://twitter.com/share?ref_src=twsrc%5Etfw" class="twitter-share-button" data-text="クラウド選定基準 in Japan #sreinfrasystemjp"  data-url="https://www.sre-infra-system.jp/odai/cloud" data-show-count="false">Tweet</a>
    <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
  </div>
  <div>
    <div class="fb-like" data-href="https://www.sre-infra-system.jp/odai/cloud" data-layout="button_count" data-action="recommend" data-size="small" data-show-faces="true" data-share="true"></div>
  </div>
  <div>
    <a href="http://b.hatena.ne.jp/entry/s/www.sre-infra-system.jp/odai/cloud" class="hatena-bookmark-button" data-hatena-bookmark-layout="basic-label-counter" data-hatena-bookmark-lang="ja" title="このエントリーをはてなブックマークに追加"><img src="https://b.st-hatena.com/images/entry-button/button-only@2x.png" alt="このエントリーをはてなブックマークに追加" width="20" height="20" style="border: none;" /></a>
    <script type="text/javascript" src="https://b.st-hatena.com/js/bookmark_button.js" charset="utf-8" async="async"></script>
  </div>
</div>
<style>
  .sns {
    margin-top: 2em;
    padding: 20px 0;
  }
  .sns div {
    display: inline-block;
  }
  .fb_iframe_widget > span {
    vertical-align: baseline !important;
  }
</style>
