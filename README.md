XC3AutoCraft
====

**XC3AutoCraft** は**ゼノブレイド３のアクセサリークラフトを全自動で操作**するためのツールです。
PC上でゲーム状況を認識する**XC3StateDetector**と
Nintendo Switchにボタン入力を送信する**XC3KeyCommander**の
2つのプログラムが連動し、予め設定したアクセサリーが出るまでクラフトを続けます。

## デモ
![XC3StateDetector_DEMO](https://github.com/eightgamedev/XC3AutoCraft/assets/47023171/b880efe5-ce19-4a58-859e-3694353766d1)

## 紹介動画
[アクセサリーを完全自動化！ XC3AutoCraft 紹介動画](https://www.youtube.com/watch?v=fSytPmym8lA)

## このアプリについて
- このアプリの他にArduino等のいくつかの機器が必要になります。予めご了承ください。
- アクセサリークラフトに特化しているのでユーザーはマクロを作る必要がありません。
- アクセサリーの**認識精度100%**※
※作者の環境での精度です。認識バグなどありましたらご報告いただけると幸いです。
- 画面上の仮想JoyConを**クリックで操作**することでもボタン入力ができます。 
ちょっとした操作なら物理JoyConに持ち替える必要がありません。
- 1回のクラフトあたりの入手確率を表示。確率の合計を見てどのアクセサリーを選べばよいか参考にできます。
- **特殊効果に関わらずゾロ目ステータス**のアクセサリーが欲しい場合はチェックを入れるだけで設定できます。
- 目標のアクセサリーの条件を**CSV, JSONに保存・読み込み**ができます。
(読み込みはドラッグアンドドロップにも対応)
- 自動クラフト開始時に4種類の画面(タイトル画面、フィールド、休憩ポイント、アクセサリークラフト)を認識します。
また、休憩ポイント、アクセサリークラフトのそれぞれの画面ではカーソルの位置も認識します。
細かい調整が面倒な人でもストレスフリーで開始できます。
- Windowsのトースト通知でアクセサリーの完成をお知らせ。完全放置で他の作業ができます。
- **日本語と英語に対応**しています。

## 必要なもの
- キャプチャーボード (解像度1920x1080)
- HDMIケーブル 1本 (NintendoSwitch-キャプチャーボード間)
- Arduino Leonardo (Atmega32u4)
- FT232RL USB-TTLシリアル変換アダプターモジュール(以下FT232RLと呼称)
- オス-メスジャンパーワイヤー 3本
- USB Type-A ⇔ Micro USB Type-B ケーブル 2本(以下USBケーブルと呼称)

## 推奨環境
- Windows10, Windows11 (64bit)
- Arduino IDE 1.8.13
- Arduino AVR Boards 1.8.3

## ダウンロード
こちらから最新版の**XC3AutoCraft.zip**をダウンロードしてください。

[https://github.com/eightgamedev/XC3AutoCraft/releases/tag/v1.0.0](https://github.com/eightgamedev/XC3AutoCraft/releases/tag/v1.0.0)

## 機器の準備
1. Arduino LeonardoとFT232RLをジャンパーワイヤー3本で接続する。
接続箇所は以下の表の通りです。基盤に印字されている文字を確認し接続してください。

| Arduino Leonardo | FT232RL |
| ---- | ---- |
| GND| GND |
| Tx | Rx |
| Rx | Tx |
2. Arduino IDE 1.8.13をダウンロードします。
もしPCにインストール版のArduinoを既にインストールしており、PC環境を汚したくない場合はportable版をおすすめします。
3. (portable版の場合)arduino.exeと同じ階層にportableという名前のフォルダを新規作成する。
4. hardware/arduino/avr/boards.txt をテキストエディタ(VSCodeなど)で開き、4箇所の数値を変更する。もしくは本アプリ付属のboard.txtで上書きする。
285行目: leonardo.vid.1=0x0f0d
286行目: leonardo.pid.1=0x0092
311行目: leonardo.build.vid=0x0f0d
312行目: leonardo.build.pid=0x0092
5.  arduino.exeを起動し「スケッチ」-「ライブラリをインクルード」- 「ライブラリを管理...」でライブラリマネージャを起動、「NintendoSwitchControlLibrary」と打ち込んで「NintendoSwitchControlLibrary」を「インストール」する。
6. XC3KeyCommanderフォルダを portable/sketchbook に配置しXC3KeyCommander.inoを開く。
(新規ファイル作成後、コードをコピー＆ペーストしてもよい)
7. Arduino LeonardoとPCをUSB接続する。
7. 「マイコンボードに書き込む」ボタンをクリックする。
8. 「ツール」-「ボード情報を取得」で下記のようになっていることを確認する。
BN: Arduino Leonardo
VID: 0f0d
PID: 0092
SN: HIDGF
9. Nintendo SwitchのドックとArduino LeonardoをUSBケーブルで接続する。
10. FT232RLとPCをUSBケーブルで接続する。
11. キャプチャボードとNintendo SwitchをHDMIケーブルで接続する。
12. キャプチャーボードとPCを接続する。

## 使い方
1. XC3StateDetector.exeを起動する。
2. 希望のアクセサリー、アクセサリーの種類、キャプチャボード、シリアルポートを選択する。 
3. 「次へ」のボタンをクリックする。
4. キャプチャーボードからの映像が表示されるまで待機する。
5. ゼノブレイド３を起動し、任意の休憩ポイント前でセーブする。
6. 「自動クラフト開始」のボタンをクリックする

## Q&A
| Q | A |
| ---- | ---- |
| 仮想JoyConが全く反応しない | 機器の準備が正しいかご確認ください。<br>「Nintendo Switch 自動化」と検索すると詳しく説明されているサイトがあるので参考になるかもしれません。 |
| 設定項目が多くて面倒 | 「アプリ」-「環境設定」でデフォルトのキャプチャーボードとシリアルポートを設定できます。
| アプリがエラーを吐いて起動しない | config.iniがXC3StateDetector.exeと同じフォルダにあるか確認してください。 |
| 休憩ポイントの前で自動クラフトが止まる | 休憩ポイントのメニューからセーブをするとキャラクターが休憩ポイントに対して背を向けた状態になるようです。自動クラフト開始前はフィールドでセーブするようにしてください。 |
| CSV とJSON の違いは何 | CSVにはアクセサリーの特殊効果とステータスの種類を保存されます。<br> JSONにはアクセサリーの特殊効果、ステータスの種類、作るアクセサリーの種類、特殊効果にかかわらず全て同じ種類のステータスのアクセサリを希望するかどうかの設定 が保存されます。|


## 注意事項
1. **保証および責任の免除:** このアプリケーションは無保証で提供され、特定の目的に対する適合性も含め、いかなる保証もありません。利用者は自己のリスクでご利用ください。
2. **データ損失および機器の損傷:** Nintendo Switchの操作に関連するあらゆる損害やデータの損失に対して、作者および関連する人物は一切の責任を負いません。
3. **法的な制約の遵守:** このアプリケーションの使用は、地域および国の法的な制約に従う必要があります。Nintendo Switch利用規約 第1条第5項の「任天堂の許諾を受けていない本ゲーム機の周辺機器を使用しないこと」には該当するおそれがあります。Nintendo Switchの利用規約に違反する可能性がある場合は、使用を控えてください。

以上の点を十分に理解し、同意いただいた上で、このアプリケーションをご利用ください。作者および関連する人物は、いかなる事態においても利用者に対して一切の責任を負いません。

## ライセンス
このアプリケーションはMITライセンスで提供しています。詳しくはLICENCEファイルをご確認ください。

## クレジット
画像提供：[ゼノブレイド3 アクセサリークラフトの効率を上げる便利ツールが完成しました！](https://hyperts.net/xenoblade3-craft-tool/)

## 使用ライブラリ
XC3StateDetectorは以下のMITライセンスライブラリを使用しています。
- [OpenSiv3D](https://github.com/Siv3D/OpenSiv3D)
- [doctest](https://github.com/doctest)

OpenSiv3Dを含む各ライブラリのライセンス情報につきましてはXC3StateDetector起動後F1キー、または画面上部のヘルプ->ライセンス情報からも確認することができます。

XC3KeyCommanderは以下のMITライセンスライブラリを使用しています。
- [NintendoSwitchControlLibrary](https://github.com/lefmarna/NintendoSwitchControlLibrary)

## 問い合わせ
質問・バグ報告・改善案などがありましたらIssueを作成するか[Twitterアカウント @ito_eight](https://twitter.com/ito_eight)のDMにてお知らせください。