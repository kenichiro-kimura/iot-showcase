# B-1 SORACOM Beam でデータをクラウドAPIへ送る

簡易位置情報取得機能でボタンを押した位置が取得できます。

SORACOM Harvest Dataでも地図上に表示することができますが、ここではSORACOM Beamを用いてクラウドAPIにデータを送信することでハンズオン参加者全員の位置情報を1つの地図に表示してみます。

## SORACOM Beam とは

SORACOM Beam はIoT デバイスにかかる暗号化等の高負荷処理や接続先の設定を、クラウドにオフロードできるサービスです。Beam  を利用することによって、クラウドを介していつでも、どこからでも、簡単に IoT  デバイスを管理することができます。大量のデバイスを直接設定する必要はありません。



詳細は [SORACOM Beam サービス紹介ページ](https://soracom.jp/services/beam/) をご覧ください。

## SORACOM Beamの設定

先ほどHarvestの設定を行ったSIMグループの設定画面で、「SORACOM Beam設定」 をクリックします。

![go-beam.png](https://docs.google.com/drawings/d/e/2PACX-1vRuEF4DnggwpdDWPs81LIL1aAm78asXXrrAwhaaEg0HQotztFb3l7j9M-f11dYV6ztMMjFH1XS1nj2Y/pub?w=407&h=400)

[+] をクリックし、プルダウンから「UDP → HTTP/HTTPSエンドポイント」を選択します。

![add-beamsetting.png](https://docs.google.com/drawings/d/e/2PACX-1vSJlDQcfbK63HkDYaNclIIn13oHmYReE4gEFKMfBZGZsiSsTASY5fPPCbnW9YB7uZNsTQae8Lt0mw9Z/pub?w=620&h=511)

SORACOM Beamの設定をします。

- 設定名: 任意の名前。**右のスライダーを「ON」にする**
- 転送先: プロトコルを「https」、ホスト名を「84szdth0th.execute-api.ap-northeast-1.amazonaws.com」、パスを「/test/items/」にする
- ヘッダ操作: IMSIヘッダ、IMEIヘッダをONにする

![beam-setting.png](https://docs.google.com/drawings/d/e/2PACX-1vQXhaVHHeq8_z8CMaZk1OZQdvpr_lQvIz66PpJeEiJgw3icGSU6YGluDIfe79h0TgZROUOM6UQWFXih/pub?w=460&h=714)

* ヘッダ操作: 署名ヘッダ付与を「ON」にします
* 事前共有鍵：[＋]を押し、事前供給鍵を作成します。認証情報IDは任意の文字列、概要は空欄、事前共有鍵を「XXXX」(当日スタッフから入手してください)を設定し、「保存」を押します。作成後、今作った事前共有鍵の認証情報IDを選択してください。

![psk.png](https://docs.google.com/drawings/d/e/2PACX-1vRhHTp07U28s6n438o_eNRTQtPiCnmxnENot51Tcvw0XIbNUuTVGhlAKjfmFsNARJD6kfcgYAOJif98/pub?w=874&h=834)

* カスタムヘッダ: [＋]を押し、カスタムヘッダを追加します。アクションは「追加」、ヘッダ名は「x-soracom-button-name」、値はあなたのお名前など分かりやすい文字を入力してください。これがハンズオン結果画面の地図と一覧に表示されます。
  英数字以外を入力される場合は[こちらのページ](https://tech-unlimited.com/urlencode.html)を利用してURLエンコードした値を入力してください。
  入力が終わったら「作成」を押します。

![custom-header.png](https://docs.google.com/drawings/d/e/2PACX-1vQY_6S_Cyq-6fLnYXrZnLUksqNYQDZJmxSHcpJKNI1E6WPrrAGKiQGlFoV9ip6RGo-kfit4JwkNJcex/pub?w=614&h=758)

ここまで設定したら、「保存」を押してSORACOM Beamの設定を反映させます。



<h2>ボタンを押してデータを確認する</h2>

設定が完了したら、ボタンを押してみましょう(single/double/longいずれでも結構です)。

設定が正しく行われていれば、[こちらの確認画面](http://soracom-map-20200307111440-hostingbucket-test.s3-website-ap-northeast-1.amazonaws.com/)にあなたのお名前(x-soracom-button-nameで設定した値)と簡易位置情報で取得した位置情報、取得日時が一覧に表示され、さらに地図上にピンが表示されます。



![map-result.png](https://docs.google.com/drawings/d/e/2PACX-1vROODlnOKy6Ii4y9texBB73dFfFORrDsvp0I-910JQb-Rq0zDMdSqe98sSaClISFn3DFnRzhlkeiMXI/pub?w=956&h=632)



* この確認画面は本日のハンズオンの参加者皆さんの情報が全て表示されますので、あなた以外の参加者の情報も表示されています

* データは30秒に1回自動でリフレッシュされますが、お急ぎの場合は「最新データ取得」を押してください

  

# 以上で本ページの作業は完了となります

## トラブルシュート

* **位置情報が表示されない**
    * SORACOM Harvest Data でデータが表示されているか確認してください。
    * SORACOM Beamの設定でサーバ名やパスがまちがっていないか確認してください。
* 事前共有鍵がまちがっていないか確認してください。
    * 追加ヘッダのx-soracom-button-nameの値に英数字と「%」以外が入っていないか確認してください。日本語を入れる場合はURLエンコードしてください。
    
* **名前が表示されず、数値が表示される**
    * SORACOM Beamの設定で追加ヘッダに「x-soracom-button-name」を追加しているか確認してください。この値がない場合、ボタンのIMSIの値が表示されます。
