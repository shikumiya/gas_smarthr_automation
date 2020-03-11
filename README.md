# SmartHR 申請処理自動化

SmartHRの電子申請にかかる添付ファイルのダウンロード・解凍・Google Driveへのアップロード、申請ステータスの変更を自動化する。

* Google Drive
* Google Spreadsheet
* Google Apps Script
* imaya/zlib.js
* polygonplanet/encoding.js

# 課題

クラウド人事労務ソフトの[SmartHR](https://smarthr.jp/)では電子申請が行えます。
SmartHRからの電子申請には電子証明書を取得して電子申請を行えるようにする必要があります。

電子申請された手続は、SmartHR上で進捗管理ができ、完了した手続に関しては
SmartHRの画面上から公文書のリンク経由でファイルを直接ダウンロードすることができます。

この機能について申請一つ一つを見ればとても便利なのですが、1ヶ月の間に大量の申請を行うような入退社が多い大企業や、複数の企業を取り扱う社労士、経営管理コンサルタントにとっては不便な点もあります。

公文書の添付ファイルはe-Govで手続を行った時と同様に圧縮されたzipファイルで、SmartHR上から検索することはできません。
従って、そのファイルに後日アクセスすることを考えると、SmartHR外にファイルを保存しておく必要があります。

外部にファイルを保存する場合、手続きごとに画面を切り替えてファイルをダウンロードし、そのファイルを別途社内で用意したストレージに格納することが必要です。この処理を実際に手順単位で書き下ろすと以下の通りです。

【業務手順】
1. 顧客毎に用意されたSmartHRの専用URLからログイン
2. 申請の一覧を参照し、特定のステータスのデータを検索
3. 公文書やお知らせといった添付ファイル(zip)をダウンロード
4. ダウンロード・解凍したファイルをGoogle Drive上にアップロードして更にリネーム
5. 申請データをアーカイブ
6. スプレッドシートのステータスを変更

上記業務手順をGASで自動化します。