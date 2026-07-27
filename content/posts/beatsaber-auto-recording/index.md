+++
title = 'BeatSaberを怠惰に録画する'
date = '2026-07-27T15:18:40+09:00'
draft = false
+++

はじめまして、しじりむです。

突然、今年の１月ころにBeatSaberのプレイ動画を投稿したいと思い立ちました。
しかし、良いプレイはいつ出来るかなんてわからないもの。常時録画から切り出すのは非常にめんどくさいです！
そこで、できるだけ何もせずにプレイ動画を残せるよう、色々試してみました。

## 対象
 - BeatSaberのプレイを普通に録画出来る人（camera2, アバターなどなど)
 - 怠惰のために環境構築出来る人
 - 自分の環境に読み替えられる人

## 筆者の環境
 - Ubuntu 24.04 X11
 - Steam deb板
 - BeatSaber v1.40.8
 - BSManager v1.5.6
 - OBS 32.2.1 Flatpak板

## 時間のない人のための要点
 1. [github.com/qqrz997/OBSControl](https://github.com/qqrz997/OBSControl) を使う
 2. 設定は起動する前に ```UserData/OBSControl.json``` を触ると早い

# では、時間のある人のために

## MODを入れる
依存を入れてしまいましょう

BSManagerならMODのセクションからそのままインストールできます。
 - <https://github.com/Auros/SiraUtil>
 - <https://github.com/monkeymanboy/BeatSaberMarkupLanguage>

つぎに本体を入れます。
[release](https://github.com/qqrz997/OBSControl/releases) から落として展開したプラグインを、自分がつかっているBeatSaberのPluginsにコピー
作者さんは1.40.4でテスト済みとのことですが、1.40.8でも動作しました。
[Zingabopp/OBSControl](https://github.com/Zingabopp/OBSControl)が本流だったようですが、こちらはBeatSaber v1.21.0までの対応のようです。

ここで一度、設定ファイルを生成してもらうためにBeatSaberを起動して閉じてください。

## OBSを設定する
のは、OBSControlの[README](https://github.com/qqrz997/OBSControl) を見るのが明らかに早いので省略します。
注意点は、必ずApplyを押すことです。パスワードはランダム生成し、Applyを押して確定してください。

## BeatSaberの設定をする
まず先程OBSで設定したWEBSocketのパスワードを入力します。

VR内のMODSettingsからも入力できるのですが、それはめんどくさいので、直接設定ファイルをいじります。

BeatSaberが落ちていることを確認し、ディレクトリにある```UserData/OBSControl.json``` の中を編集します。

```"WsIpAddress": "127.0.0.1",```となるように入力

```"ServerPassword": "",``` の部分に先程設定したパスワードを入力です。

また気が向けばファイルフォーマットも編集して良いでしょう。
筆者は
```"RecordingFileFormat": "?@{yyyyMMdd_HHmmss}__id-?I__diff-?D__score-?s__acc-?%__end-?E__?N{30}<__mods-[?M]><__?F>",```
を使っています。

## 動作確認
OBSのWebSocket Server Settingsを開いた状態で、BeatSaberを起動してください。

そうすると、Connected WebSocket Sessions にBeatSaberが接続されたことが解ると思います。

また、プレイすると自動で楽曲ごとに動画ファイルが出来るはずです。

もし接続されなかったときには、パスワードが正しく入力できているか、OBSでしっかりとApplyを押しているか、jsonファイルをBeatSaber起動中に編集していないかは確認する価値があると思います。

## 問題点
びっくりする程にストレージ容量を食います。
１曲1GBくらいの気持ちで挑んだほうが良いです。
近い将来、自動でファイル整理してくれるスクリプトを作りたいところです。

## その他
 - 1月からはや半年、ようやくYoutubeチャンネルを開設出来ました。良ければフォローしてください。<https://www.youtube.com/@shijiRim>
 - 不明点、記事に問題などあれば、<https://x.com/shijiRim> へDMお願いします。
