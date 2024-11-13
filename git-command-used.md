### はじめに

どうも、yukiです。

今回は最近使用したgit コマンドをまとめてみました。

### git pushを取り消す

- 自分しか変更しないことがわかっているブランチだったので、`git reset`にて対応しました。
- 以下のコマンドで前のコミットの状態に戻る。`--soft`はローカルでの変更等を残す、`--hard`はcommit,add,ソース含め全部戻す。

```
 $ git reset --soft HEAD^

```

- `-f`で強制的にカレントブランチをpushすると、履歴を残さず修正できます。

```
 $ git push -f origin HEAD
```

<figure class="figure-image figure-image-fotolife" title="Pull request上では記録に残っていました。">[f:id:yuki0224_1:20240913155344p:plain:alt=Pull requestに記録が残っていることを示す写真]<figcaption>Pull request上では記録に残っていました。</figcaption></figure>

- gitに履歴を残して修正したい場合は、`git revert`を使います。複数人で作業しているブランチだと、どちらの方法もコンフリクトがこわいですね。

### 削除したリモートブランチがローカルに残ってる

- `git branch -a`で、削除したブランチがローカルにたくさん残っていることに気付きました。
- feachするときに`-prune`をつけて解決。

```
$ git fetch --prune ( git fetch -p )
```

- 毎回オプションつけるのめんどくさいので、fetch時に自動でpruneしてくれるよう.gitconfigに設定しました。

```
[fetch]
    prune = true
```

### 参考

- [git pushを取り消す方法](https://qiita.com/S42100254h/items/db435c98c2fc9d4a68c2)

- [Gitのリモートブランチを削除するまとめ](https://qiita.com/yuu_ta/items/519ea47ac2c1ded032d9)

### おわりに

ガチャガチャしているうちに、座学で得た知識の定着が始まってきました。HEAD、index、リモート/ローカルブランチとか。

`git revert`の理解が浅いので、どっかで実験したいなあ。
