---
title: sysの使い方: 「circular import error」の対処法
---
### はじめに
今回はPythonビルドインのモジュールである`sys`と`argparse`について得た知見をまとめていきます。

### argparse
例えば、`hoge.py -n 2`のような引数を受け取るプログラムを作成しているとします。
今回はargparseを使って、引数オプションを受け取る形にします。
引数の範囲は1~6の整数であるとします。
ArgumentParser().add_argument()でtypeに自作の関数を指定し、
値をバリデーションしましょう。
以下、自作の関数例。

```python
def validate_sample(num):
    try:
        num = int(num)
        if 1 <= num <= 6:
            return num
        else:
            raise ValueError
    except ValueError:
        raise argparse.ArgumentTypeError(
            f"{num} is neither a num number (1..6) nor a name"
        )
```
簡単な説明
引数が1~6の整数でない場合、ValueErrorをraiseし、例外処理で
ArgumentTypeErrorをraiseします。

typeに指定した関数がArgumentTypeError, TypeError, 
または ValueError 型の例外を送出した場合、parserはその例外をキャッチして
エラーメッセージを表示します。
具体的には、errorメソッドの引数messageにエラーメッセージが入ります。


実際に使用してみましょう。簡単にテストメソッドを実装してみました。

```python
def parse_arguments():
    parser = argparse.ArgumentParser()
    parser.add_argument(
        "-n",
        type=validate_sample,
        default=1,
    )

    return parser.parse_args()
```

usage: sample.py [-h] [-n]
calendar.py: error: argument -n: 22 is neither a num number (1..6) no
r a name


さて、このエラーメッセージを少しカスタマイズしてみましょう。
完成図は以下のようにしてみましょう。
argument -m/--month: 22 is neither a num number (1..6) no
r a name

まずはargparse.ArgumentParser()を継承したカスタムクラスを作成します。
errorメソッドの引数messageにエラーメッセージが入ります。
そこでerrorメソッドをオーバーライドし、エラーメッセージをカスタマイズします。

```python
class CustomArgumentParser(argparse.ArgumentParser):
    def error(self, message):
        print(message, file=sys.stderr)
        sys.exit(2)
```
シンプルにエラーメッセージを標準出力し、プログラムを終了させます。
sys.exitの引数2はコマンドライン引数のエラーを示す慣習的な値です。
では、再度実行。

argument -m/--month: 22 is neither a month number (1..12) nor a name

いいですね。少しの違いですが、エラーメッセージ表示について理解が深まったのではないでしょうか。

