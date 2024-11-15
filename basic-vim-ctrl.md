---
title: vimの基本操作
---
# はじめに

どうも、yukiです。<br>
今回は最近vimに入門した自分が、基本操作についてまとめてみました。

※vimとはテキストエディタの一種です。コマンドを駆使することで、キーボードのホームポジションからほとんど動かずに操作ができるといった特徴があります。

**これからvimを学習しようという方は、まず「vimtutor」から取り掛かることをおすすめします。**

<br>
↓ターミナルに以下のように入力し、エンターを押して始めます。
```
$ vimtutor

```


**このチュートリアルの文章自体をvimで編集しながら進めていくので、ハンズオンでvimの使い方を学ぶことが出来ます。**


紹介が終わったところで、さっそく本題へ参りましょう！
# 基本操作



## モードについて
- vimにはカーソルを移動するためのモードや、文字を入力するためのモードがあります。

| モード       | 説明                             | 切り替えキー |
|------------------|----------------------------------|--------------|
| ノーマルモード   | カーソル移動やコマンド実行を行うモード | `esc`       |
| インサートモード | 文字入力を行うモード                | `i`         |
| ビジュアルモード | 範囲を指定するモード            | `v`         |
| コマンドモード   | 指定のコマンドを入力するモード | `:`         |

- 基本的にはノーマルモードから他のモードに移行して使用する機会が多いと思いますので、困ったら`esc`でノーマルモードに戻りましょう。


## コマンドについて
- **コマンドによっては、コマンドの前に数字を入力することで、その数字分効果が期待できるものがあります。**

&emsp;&emsp;例. `5h` → カーソル位置から5つ左に移動、`4dd` → カーソル位置から4行削除

### 起動
| コマンド       | 説明                             |
|------------------|----------------------------------|
| vim hoge.txt    | hoge.txtを開く(読み書き可能) |

### カーソル移動

| コマンド| 説明 |
| --- | ------------ |
| `h` | 左にカーソル移動|
| `j` | 下にカーソル移動|
| `k` | 上にカーソル移動|
| `l` | 右にカーソル移動|
| `w` | 次の単語へ移動|
| `b` | 前の単語へ移動|
| `e` | 次の単語の最後へ移動|
| `^` | 行頭へ移動|
| `$` | 行末へ移動|
| `gg` | ページの一番上に行く|
| `G` | ページの一番下に行く|

### 入力

| コマンド| 説明 |
| --- | ------------ |
|`i`|カーソル位置から入力|
|`a`|カーソル位置の次の文字から入力|
|`o`|改行して入力|
|`O`|上に行を挿入して入力|
|`A`|行の最後から入力|
|`I`|行の最初から入力|




### 削除/変更

|コマンド|説明|
|---|---|
|`x`|カーソル位置の文字削除|
|`dw`|次の単語まで削除|
|`dd`|カーソルがある行を削除|
|`d$`|カーソルがある行のカーソルより後ろを削除|
|`ce`|単語の末尾まで変更|
|`cc`|行全体を削除してインサートモードに入る|

### コピー/ペースト

|コマンド|説明|
|---|---|
|`y`|コピー|
|`yy`|カーソルがある行をコピー|
|`p`|カーソルの後ろにペースト|
|`P`|カーソルの手前にペースト|

### 検索/置換

|コマンド|説明|
|---|---|
|`/hoge`|hogeを下方向検索|
|`?hoge`|hogeを上方向検索|
|`n`|次の検索結果に移動|
|`R`|カーソル位置から入力した文字で既存のテキストを置換|
|`:s/変更前の単語/変更後の単語`|カーソル行の最初にある変更前の単語を変更後の単語に置換|
|`:s/変更前の単語/変更後の単語/g`|カーソル行の全ての変更前の単語を変更後の単語に置換|





### 編集
|コマンド|説明|
|---|---|
|`u`|変更を取り消す(undo)|
|`Ctrl + r`|直前に取り消した操作をやり直す(redo)|

### ファイル操作
|コマンド|説明|
|---|---|
|`:w`| 保存 |
|`:q`|ファイルを閉じる|
|`:wq`|保存してファイルを閉じる|

# おわりに
基本的なコマンドを押さえたら、応用的なコマンドにも挑戦してみたいですね！

もし誤記、間違い等ありましたらご指摘よろしくお願いいたしますm(__)m













```
