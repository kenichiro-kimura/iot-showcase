# C-2 SORACOM Funk から 関数(Function) を呼び出しデバイスを制御する

本ページでは、ボタンを押した時に先ほど作成した Function を呼び出すために、SORACOM Funk の設定を行います。
C-1 の最後にメモしておいた URL を使いますので、もしメモしていなかった場合は GCP コンソール で確認してください。

## グループの設定
作業A で作成したグループを使用します。

[SORACOM ユーザーコンソール](https://console.soracom.io/){:target="_blank"} を開き、SIM 管理画面でボタンの SIM のグループ名をクリックし、グループ詳細画面を開きます。
> または、SORACOM ユーザコンソール 左上の「≡ Menu」から `SORACOM Air for Cellular` ＞ `SIM グループ` を開き、ボタンに割り当てているグループ詳細画面を開きます。

### SORACOM Funk 設定
「SORACOM Funk 設定」を開き、下記のように設定します。

- サービス: Google Cloud Functions
- 送信データ形式: JSON
- 関数のURL: C-1 でメモした URL

![Funk 設定1](images/soracom-funk.png)

最後にグループ設定の一番下部にある「Unified Endpoint 設定」を開き、フォーマットから 「SORACOM Funk」を選択して、「保存」を押します。

![Unified 設定](images/soracom-unified.png)

## ボタンを押して 関数(Function) を呼び出し、デバイスが連動したかどうか確認する

ボタンを押して LED が緑色に光れば、呼び出し成功です。

デバイスが応答したかどうかを確認しましょう。

> シングルクリックで２秒間、ダブルクリックで４秒間、ロングクリックで５秒間、ファンが回ります。

![ボタンとファン](images/button_and_fan.gif)

## 以上で本ページの作業は完了となります

## トラブルシュート

* ボタン押下の結果、LED が赤になってしまう
    * A: 15秒以上経ってから LED が赤になる場合は、電波状況が悪い場合があるため再度試してみてください
    * B: 10秒程度で LED が赤になる場合は Function 設定の見直しが必要な場合があります
        * URL は正しく指定出来ているか
        * Function のコードが正しくコピー出来ているか
        * package.json で追加パッケージが指定されているか
        * 実行関数を `main` に書き換えたか
        * Function のページで「ログを表示」をクリックし、メッセージを確認

## 参考情報
デバイス側のサンプルコードは以下を参考にしてください。

- SORACOM Beam を使って Google Cloud IoT Core の MQTT Broker に接続します
- /devices/wiolte/commands 以下の topic を subscribe します
- クリックのタイプ(1 or 2 or 3)に応じて、異なる動作をするようになっています

<script src="https://gist.github.com/j3tm0t0/0c1470134cefbe87b876eaf69a94b460.js"></script>
